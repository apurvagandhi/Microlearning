# External Setup Guide - What to Do Outside This Repository

This guide covers all the setup you need to do OUTSIDE this repository to ensure smooth hackathon operations.

---

## 1. 🌐 GitHub Organization & Repository Setup

### Create GitHub Organization (Optional but Recommended)

1. Go to https://github.com/organizations/new
2. Choose organization name (e.g., `nc-state-micro-learning`)
3. Set it to Public
4. Add all team members
5. Organize repositories if needed

### Invite Team Members

1. Go to Organization Settings → Members
2. Invite all 14 students as collaborators
3. Set roles:
   - **Owners** (2): You and 1 student lead
   - **Maintainers** (2-3): Technical leads
   - **Members** (11): Regular contributors

### Configure GitHub Repository Settings

1. Go to Settings → General
   - Description: "Micro-learning platform for open-source education"
   - Website: (leave for now)
   - Topic: "open-source", "education", "micro-learning"
   - Make public

2. Go to Settings → Collaborators & teams
   - Ensure all students have "Write" permission

3. Go to Settings → Branches
   - Add branch protection for `main`:
     - Require pull request before merging
     - Require 1 approval
     - Dismiss stale reviews
     - Require status checks to pass

4. Go to Settings → Actions
   - Enable GitHub Actions
   - Allow all actions

---

## 2. 📧 Communication Setup

### Create Slack/Discord Workspace (Optional but Highly Recommended)

#### Slack
1. Go to https://slack.com/create
2. Create workspace (e.g., "NC State Micro Learning")
3. Invite all students
4. Create channels:
   - `#general` - Announcements
   - `#help` - Questions
   - `#frontend` - Frontend team
   - `#backend` - Backend team
   - `#devops` - DevOps team
   - `#random` - Off-topic
   - `#standup` - Daily standups
5. Install GitHub app: `/github subscribe`

#### Discord
1. Go to https://discord.com/servers/create
2. Create server
3. Invite all students
4. Create similar channels
5. Add GitHub bot integration

### Email Distribution List (Optional)

If your institution supports it:
- Create mailing list for announcements
- Add all 14 students + instructors

---

## 3. 🔑 Third-Party Accounts

### Deployment Platforms

#### Vercel (Frontend Hosting)
1. Go to https://vercel.com/signup
2. Sign up with GitHub
3. Connect GitHub account
4. Create team (optional)
5. Note: No payment needed for free tier

#### Railway (Backend Hosting)
1. Go to https://railway.app/login
2. Sign up with GitHub
3. Create account
4. Get $5 free credit on signup
5. Add payment method (optional)

**OR**

#### Render (Alternative Backend)
1. Go to https://render.com
2. Sign up with GitHub
3. Create account
4. Free tier available

### Docker Hub (Optional)
1. Go to https://hub.docker.com/signup
2. Create account
3. Create a repository for your image
4. Link to GitHub (optional, for auto-build)

### Database-as-a-Service (Optional Alternative)

If you prefer managed database:
- **Railway**: Includes PostgreSQL
- **Render**: Includes PostgreSQL
- **ElephantSQL**: Free PostgreSQL tier (but limited)

---

## 4. 📊 Project Management (External to GitHub)

### GitHub Projects Board
- Recommended: Use GitHub Projects (free, integrated)
- Alternative: Trello, Asana, Linear (if preferred)

### GitHub Discussions
- Enable in Repository Settings → Features
- Create discussion categories

### GitHub Wiki
1. Go to Repository → Wiki tab
2. Create Home page with links to docs
3. Useful for diagrams and architecture

---

## 5. 🔧 Local Development Setup (For Each Student)

Before Day 1, ensure all students have:

### Required Software
- [ ] Git: https://git-scm.com/download
- [ ] Node.js 18+: https://nodejs.org/
- [ ] npm 7+: (comes with Node.js)
- [ ] Docker (optional): https://www.docker.com/products/docker-desktop
- [ ] VS Code: https://code.visualstudio.com/
- [ ] PostgreSQL: https://www.postgresql.org/download/ (or use Docker)

### VS Code Extensions to Install
- [ ] ESLint
- [ ] Prettier
- [ ] Thunder Client or REST Client (for API testing)
- [ ] React Developer Tools
- [ ] PostgreSQL
- [ ] Docker (if using Docker)

### Git Configuration
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@ncsu.edu"
git config --global core.editor "code"  # Set VS Code as default editor
```

### SSH Keys for GitHub
```bash
ssh-keygen -t ed25519 -C "your.email@ncsu.edu"
# Add to GitHub: Settings → SSH and GPG keys
```

---

## 6. 📚 Learning Resources (Send to Students)

### Git & GitHub
- GitHub Skills: https://skills.github.com
- Git Tutorial: https://git-scm.com/book/en/v2
- First Contributions: https://firstcontributions.github.io

### Frontend (React)
- React Official: https://react.dev
- Vite Guide: https://vitejs.dev
- TailwindCSS: https://tailwindcss.com/docs

### Backend (Node.js)
- Express.js: https://expressjs.com
- Node.js Docs: https://nodejs.org/en/docs/

### Databases
- PostgreSQL: https://www.postgresql.org/docs/
- SQL Tutorial: https://www.w3schools.com/sql/

### Docker
- Docker Getting Started: https://docs.docker.com/get-started/
- Docker Hub: https://hub.docker.com

### General
- Open Source Guide: https://opensource.guide
- Semantic Versioning: https://semver.org

---

## 7. 🔐 Security & Secrets Management

### Before Day 1

1. **Ensure no secrets in code**
   - Add `.env` to `.gitignore`
   - Create `.env.example` with placeholder values
   - Document required variables

2. **Set up secrets management**
   - GitHub Secrets for GitHub Actions
   - Vercel/Railway environment variables
   - Never commit actual secrets

3. **Create `.env.example` file**
   ```
   # Backend
   PORT=3000
   NODE_ENV=development
   DATABASE_URL=postgresql://user:password@localhost:5432/db
   JWT_SECRET=your-secret-key-here
   
   # Frontend
   VITE_API_URL=http://localhost:3000/api/v1
   ```

### GitHub Secrets (For CI/CD)

If needed for deployment:
1. Go to Settings → Secrets and variables → Actions
2. Add secrets:
   - `DOCKER_USERNAME` (if using Docker)
   - `DOCKER_PASSWORD` (if using Docker)
   - Other deployment secrets

---

## 8. 📋 Pre-Hackathon Checklist (For Organizers)

### One Week Before
- [ ] Repository created and setup
- [ ] All documentation written and committed
- [ ] GitHub Actions CI/CD pipeline tested
- [ ] Slack/Discord workspace created
- [ ] Vercel and Railway accounts setup
- [ ] All team members invited

### Two Days Before
- [ ] Send setup instructions to all students
- [ ] Verify all students have cloned repo
- [ ] Check everyone has required software installed
- [ ] SSH keys setup for each student
- [ ] First test CI/CD pipeline run

### Day Before
- [ ] Final team meeting
- [ ] Assign roles to each student
- [ ] Create initial GitHub issues (Day 1-2)
- [ ] Prepare architecture discussion
- [ ] Set up daily standup time
- [ ] Double-check all systems working

### Morning of Day 1
- [ ] Kick-off meeting
- [ ] Review timeline and goals
- [ ] Assign first tasks
- [ ] Get first commits in!

---

## 9. 🎯 Team Lead Responsibilities

### Project Manager (Pick 2 students or 1 instructor)

Daily:
- [ ] Post standup template in Discussions
- [ ] Review GitHub Projects board
- [ ] Unblock issues
- [ ] Chase down PRs for review

Weekly:
- [ ] Hold retro meeting
- [ ] Update milestone progress
- [ ] Celebrate wins

### Technical Leads (Frontend, Backend, DevOps)

Daily:
- [ ] Review PRs from team
- [ ] Help with technical issues
- [ ] Make architecture decisions

### QA Lead (Pick 1-2 students)

Daily:
- [ ] Test new features
- [ ] Create bug reports
- [ ] Verify fixes

---

## 10. 📞 Troubleshooting Resources

### Common Issues Before Starting

**Node version conflicts**
```bash
# Check version
node --version
# If wrong version, use nvm (Node Version Manager)
nvm install 18
nvm use 18
```

**Port already in use**
```bash
# Find process on port 3000
lsof -i :3000
# Kill it
kill -9 <PID>
```

**Git SSH key issues**
```bash
# Test SSH connection
ssh -T git@github.com
# Should say: Hi username! You've successfully authenticated.
```

**Database connection refused**
```bash
# For Docker PostgreSQL
docker run --name postgres -e POSTGRES_PASSWORD=postgres -p 5432:5432 -d postgres:15
```

---

## 11. 🚀 Day-by-Day External Checklist

### Day 1: Setup
- [ ] All students have cloned repo
- [ ] All software installed locally
- [ ] First commits pushed
- [ ] CI/CD pipeline running
- [ ] Standup meeting held

### Day 5: Mid-point
- [ ] 30+ issues created
- [ ] 15+ PRs merged
- [ ] Core architecture stable
- [ ] Database ready
- [ ] Frontend/backend talking

### Day 10: Launch
- [ ] Frontend deployed to Vercel
- [ ] Backend deployed to Railway
- [ ] Production database migrated
- [ ] Final demo completed
- [ ] Repository polished

---

## 12. 📞 External Communication Links

### For Instructors/Organizers
- **GitHub Org Settings**: https://github.com/settings/organizations
- **GitHub Billing**: https://github.com/settings/billing
- **Vercel Dashboard**: https://vercel.com/dashboard
- **Railway Dashboard**: https://railway.app

### For Students
- **GitHub Classroom** (if using): https://classroom.github.com
- **GitHub Notifications**: https://github.com/notifications
- **Your Profile**: https://github.com/settings/profile

---

## 13. 🎓 Educational Resources

Consider using:
- **GitHub Classroom** for assignments (https://classroom.github.com)
- **GitHub Copilot** for students (free with edu email)
- **GitHub Learning Lab** courses
- **Recorded talks** from GitHub Universe

---

## Recommended Schedule Before Hackathon

### One Month Before
- [ ] Decide on tech stack
- [ ] Create project outline
- [ ] Recruit/confirm 14 students

### Two Weeks Before
- [ ] Create repository
- [ ] Write all documentation
- [ ] Set up GitHub/Vercel/Railway accounts
- [ ] Create Slack workspace
- [ ] Prepare architecture workshop

### One Week Before
- [ ] Send repo link and setup instructions to students
- [ ] Hold orientation meeting
- [ ] Test infrastructure
- [ ] Create initial issues

### Day Before
- [ ] Final team meeting
- [ ] Confirm attendance
- [ ] Do a final system check

---

## Key Success Factors

✅ **Clear Communication** - Everyone knows what they're building
✅ **Good Documentation** - Students can find answers fast
✅ **Working CI/CD** - Catch bugs early
✅ **Free Tools** - No licensing issues
✅ **Mentorship** - Leads available for help
✅ **Realistic Timeline** - 10 days is tight but doable
✅ **Team Spirit** - Make it fun!

---

**Last Updated:** February 8, 2026

**Questions?** Create an issue in the repository or start a discussion!
