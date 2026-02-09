# Deployment Guide

Complete guide to deploying the Micro-Learning App to production on AWS.

## Deployment Architecture

```
GitHub Repository
       │
       ├─► Jenkins or GitHub Actions (CI/CD Pipeline)
       │   - Run tests
       │   - Build Docker image
       │   - Push to Docker Hub / AWS ECR
       │
       ├─► Frontend
       │   Deployment Target: AWS S3 + CloudFront
       │   - Static hosting for Angular SPA
       │   - CDN enabled
       │   - URL: https://your-domain.com
       │
       └─► Backend
           Deployment Target: AWS EC2 / ECS
           - Deploy Docker container
           - RDS PostgreSQL database
           - URL: https://api.your-domain.com
```

---

## Part 1: Frontend Deployment (AWS S3 + CloudFront)

### Prerequisites
- AWS Account with appropriate permissions
- AWS CLI installed and configured
- GitHub repository with Angular frontend code
- Domain name (optional for initial deployment)

### Step 1: Create S3 Bucket

```bash
# Create bucket (replace with your domain)
aws s3 mb s3://micro-learning-app-frontend

# Enable static website hosting
aws s3 website s3://micro-learning-app-frontend \
  --index-document index.html \
  --error-document index.html
```

### Step 2: Build Angular Application

```bash
cd frontend
npm install
npm run build

# Output is in dist/micro-learning-app/
```

### Step 3: Upload to S3

```bash
# Copy built files to S3
aws s3 sync dist/micro-learning-app/ s3://micro-learning-app-frontend --delete

# Set proper cache headers
aws s3 cp s3://micro-learning-app-frontend/index.html \
  s3://micro-learning-app-frontend/index.html \
  --cache-control "max-age=0, no-cache, no-store, must-revalidate" \
  --content-type "text/html" \
  --acl public-read --recursive
```

### Step 4: Create CloudFront Distribution

1. Go to AWS CloudFront console
2. Create new distribution
3. Set S3 bucket as origin
4. Configure settings:
   - Default root object: `index.html`
   - Error responses: Route 404 to `index.html` (for Angular routing)
5. Add custom domain if you have one
6. Create SSL certificate via ACM
7. Deploy

### Step 5: Configure Environment for Angular

Update `frontend/.env.production`:
```
NG_APP_API_URL=https://api.your-domain.com/api/v1
```

---

## Part 2: Backend Deployment (AWS EC2 or ECS)

### Option A: EC2 Deployment

#### Prerequisites
- AWS Account
- EC2 key pair created
- Security group configured

#### Step 1: Launch EC2 Instance

```bash
# Use AWS CLI or Console to launch:
# - Amazon Linux 2 or Ubuntu 20.04
# - t3.micro or t3.small (free tier eligible)
# - Security group: Allow 22 (SSH), 80 (HTTP), 443 (HTTPS)
```

#### Step 2: Set Up Environment

```bash
# SSH into instance
ssh -i your-key.pem ec2-user@your-instance-ip

# Install Docker
sudo yum update -y
sudo amazon-linux-extras install docker -y
sudo systemctl start docker
sudo usermod -a -G docker ec2-user

# Install Docker Compose
sudo curl -L \
  "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" \
  -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
```

#### Step 3: Deploy Backend via Docker

```bash
# Clone your repository
git clone your-repo-url
cd backend

# Create .env file
cat > .env << EOF
PORT=3000
NODE_ENV=production
DATABASE_URL=postgresql://user:pass@rds-endpoint:5432/micro_learning
JWT_SECRET=your-secret-key
JWT_EXPIRE=7d
CORS_ORIGIN=https://your-domain.com
EOF

# Build and run Docker container
docker build -t micro-learning-api .
docker run -d --name api \
  -p 80:3000 \
  --env-file .env \
  micro-learning-api
```

### Option B: AWS ECS Deployment (Recommended)

#### Step 1: Push Docker Image to ECR

```bash
# Create ECR repository
aws ecr create-repository --repository-name micro-learning-api

# Get login token
aws ecr get-login-password --region us-east-1 | docker login \
  --username AWS --password-stdin [account-id].dkr.ecr.us-east-1.amazonaws.com

# Tag and push image
docker build -t micro-learning-api .
docker tag micro-learning-api:latest [account-id].dkr.ecr.us-east-1.amazonaws.com/micro-learning-api:latest
docker push [account-id].dkr.ecr.us-east-1.amazonaws.com/micro-learning-api:latest
```

#### Step 2: Create ECS Cluster and Service

1. Go to AWS ECS console
2. Create cluster
3. Create task definition (specify ECR image, environment variables, port mappings)
4. Create service with Auto Scaling
5. Attach load balancer (ALB)

---

## Part 3: Database Setup (AWS RDS)

### Step 1: Create RDS Instance

```bash
# Via AWS CLI
aws rds create-db-instance \
  --db-instance-identifier micro-learning-db \
  --db-instance-class db.t3.micro \
  --engine postgres \
  --master-username admin \
  --master-user-password YourSecurePassword \
  --allocated-storage 20 \
  --publicly-accessible false \
  --vpc-security-group-ids sg-xxxxxxxx
```

### Step 2: Configure Security Group

Allow traffic on port 5432 from:
- Your EC2 security group (for backend)
- Your local machine (for development)

### Step 3: Initialize Database

```bash
# From your local machine or EC2 instance
PGPASSWORD=YourPassword psql -h rds-endpoint.amazonaws.com \
  -U admin -d postgres -f init-schema.sql
```

---

## Part 4: CI/CD Pipeline Setup

### Option A: GitHub Actions

Create `.github/workflows/deploy-aws.yml`:

```yaml
name: Deploy to AWS

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build-and-test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      
      # Frontend
      - name: Build Frontend
        run: cd frontend && npm ci && npm run build
      
      # Backend
      - name: Build Backend
        run: cd backend && npm ci && npm run build
      
      - name: Test Backend
        run: cd backend && npm run test

  deploy-frontend:
    needs: build-and-test
    if: github.event_name == 'push' && github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      
      - name: Build Frontend
        run: cd frontend && npm ci && npm run build
      
      - name: Deploy to S3
        run: |
          aws s3 sync frontend/dist/micro-learning-app/ \
            s3://micro-learning-app-frontend --delete
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
      
      - name: Invalidate CloudFront
        run: |
          aws cloudfront create-invalidation \
            --distribution-id ${{ secrets.CLOUDFRONT_DISTRIBUTION_ID }} \
            --paths "/*"
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}

  deploy-backend:
    needs: build-and-test
    if: github.event_name == 'push' && github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Docker
        uses: docker/setup-buildx-action@v2
      
      - name: Login to ECR
        run: |
          aws ecr get-login-password --region us-east-1 | \
            docker login --username AWS \
            --password-stdin ${{ secrets.AWS_ACCOUNT_ID }}.dkr.ecr.us-east-1.amazonaws.com
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
      
      - name: Build and Push Backend Image
        run: |
          cd backend
          docker build -t ${{ secrets.AWS_ACCOUNT_ID }}.dkr.ecr.us-east-1.amazonaws.com/micro-learning-api:latest .
          docker push ${{ secrets.AWS_ACCOUNT_ID }}.dkr.ecr.us-east-1.amazonaws.com/micro-learning-api:latest
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
      
      - name: Update ECS Service
        run: |
          aws ecs update-service --cluster micro-learning-cluster \
            --service micro-learning-service --force-new-deployment
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```

### Option B: Jenkins

See local docs for Jenkins setup on EC2 (available in organizer materials).

---

## Environment Configuration
PORT=3000
NODE_ENV=production

# Database (Railway auto-generates this)
DATABASE_URL=postgresql://...

# JWT
JWT_SECRET=your-production-secret-key
JWT_EXPIRE=7d

# CORS
CORS_ORIGIN=https://your-domain.vercel.app
```

### Step 3: Add PostgreSQL Database

1. In Railway Project → Add Service
2. Select "PostgreSQL"
3. Railway auto-generates `DATABASE_URL`
4. Add other required variables from Step 2

### Step 4: Configure Dockerfile

Create `backend/Dockerfile`:

```dockerfile
FROM node:18-alpine

WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm ci --only=production

# Copy source code
COPY . .

# Expose port
EXPOSE 3000

# Start server
CMD ["node", "src/server.js"]
```

### Step 5: Deploy

1. Push changes to GitHub
2. Railway auto-deploys when it detects new commits
3. Check deployment logs in Railway dashboard

### Get Backend URL

- In Railway dashboard, under your app
- Look for "Deployments" section
- Copy the URL (e.g., `https://micro-learning-api.railway.app`)
- Update frontend `.env.production` with this URL

---

## Part 3: CI/CD Pipeline Setup (GitHub Actions)

Create `.github/workflows/ci-cd.yml`:

```yaml
name: CI/CD Pipeline

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main, develop]

jobs:
  lint-and-test:
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      
      # Frontend
      - name: Install Frontend Dependencies
        run: cd frontend && npm ci
      
      - name: Lint Frontend
        run: cd frontend && npm run lint
      
      - name: Build Frontend
        run: cd frontend && npm run build
      
      - name: Test Frontend
        run: cd frontend && npm run test
      
      # Backend
      - name: Install Backend Dependencies
        run: cd backend && npm ci
      
      - name: Lint Backend
        run: cd backend && npm run lint
      
      - name: Test Backend
        run: cd backend && npm run test
  
  docker-build:
    runs-on: ubuntu-latest
    if: github.event_name == 'push' && github.ref == 'refs/heads/main'
    needs: lint-and-test
    
    steps:
      - uses: actions/checkout@v3
      
      - name: Build Backend Docker Image
        run: |
          cd backend
          docker build -t micro-learning-api:latest .
      
      # Push to Docker Hub or registry
      - name: Push to Docker Registry
        run: echo "Docker image built and ready for Railway auto-deployment"
```

---

## Part 4: Environment Configuration

### Production Environment Variables

**Frontend** (`.env.production`):
```
VITE_API_URL=https://micro-learning-api.railway.app/api/v1
VITE_APP_NAME=Micro-Learning App
```

**Backend** (`.env` on Railway):
```
PORT=3000
NODE_ENV=production
DATABASE_URL=postgresql://user:pass@host:5432/db
JWT_SECRET=very-secure-random-key-here
JWT_EXPIRE=7d
CORS_ORIGIN=https://your-app.vercel.app
```

### Secrets Management

1. Never commit `.env` files with secrets
2. Add `.env` to `.gitignore`
3. Use platform-specific secret managers:
   - **Vercel**: Environment Variables in dashboard
   - **Railway**: Variables in dashboard
   - **GitHub Actions**: Secrets in Settings → Secrets

---

## Monitoring & Logs

### Vercel Logs
1. Dashboard → Deployments → Select deployment
2. View build logs and runtime logs
3. Real-time monitoring available

### Railway Logs
1. Dashboard → Select project
2. View deployment logs
3. Stream live logs for debugging

### Database Monitoring

Monitor PostgreSQL:
```bash
# Connect to database
psql -h host -U user -d database

# Check connections
SELECT * FROM pg_stat_activity;

# Check disk usage
SELECT pg_database.datname, 
       pg_size_pretty(pg_database_size(pg_database.datname))
FROM pg_database;
```

---

## Troubleshooting Deployment

### Frontend won't deploy
- Check Vercel logs for build errors
- Verify environment variables are set
- Ensure `npm run build` works locally

### Backend crashes after deploy
- Check Railway logs for error messages
- Verify database connection string
- Check environment variables

### CORS errors in production
- Frontend URL must match `CORS_ORIGIN` in backend
- Common issue: `https://` vs `http://`

### Database connection issues
- Use Railway's auto-generated `DATABASE_URL`
- Verify whitelist/firewall settings
- Check migrations ran successfully

---

## Scaling & Performance

### Frontend Optimization
- Vercel auto-compresses and optimizes
- Enable caching in Vercel settings
- Use image optimization: `<Image>` component in Next.js or Vercel's image API

### Backend Scaling
- Monitor CPU/memory in Railway
- Enable auto-scaling if available (paid feature)
- Optimize database queries
- Use connection pooling for database

### Database
- Add indexes for frequently queried columns
- Monitor query performance
- Regular backups enabled by default

---

## Rollback Strategy

### If deployment goes wrong:

**Frontend (Vercel):**
1. Dashboard → Deployments → Previous deployment
2. Click "..." → Redeploy
3. Reverted in seconds

**Backend (Railway):**
1. Dashboard → Deployments
2. Click previous deployment
3. Select "Rollback"
4. Confirm

---

## Cost Estimates (Monthly)

| Service | Cost | Notes |
|---------|------|-------|
| Vercel | $0 | Free tier sufficient |
| Railway | $5-10 | Free tier with $5 credit |
| PostgreSQL | Free | Included with Railway |
| Domain | ~$12 | Namecheap/GoDaddy |
| **Total** | ~$17 | Fits hackathon budget |

---

## Post-Deployment Checklist

- [ ] Frontend loads without errors
- [ ] Backend API responds to requests
- [ ] Database migrations completed
- [ ] Environment variables set correctly
- [ ] CORS configured properly
- [ ] Authentication working
- [ ] Images/assets loading
- [ ] Error logging enabled
- [ ] Monitoring alerts configured
- [ ] Backup strategy in place

---

## Emergency Contacts

- **GitHub Status**: https://www.githubstatus.com
- **Vercel Status**: https://vercel-status.com
- **Railway Support**: https://railway.app/support

---

**Last Updated:** February 8, 2026
