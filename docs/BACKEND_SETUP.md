# Backend Setup Guide

> **📢 Backend Tech Decision**: Join the Tuesday GitHub Discussion to vote between **Python + FastAPI** or **Java + Spring Boot**. See [ORGANIZER_NOTES.md](ORGANIZER_NOTES.md) for discussion details.

## Prerequisites (Common)
- **PostgreSQL 12+** - [Download](https://www.postgresql.org/download/) or use Docker
- **Docker** (recommended for database)
- **Git**

## Option 1: Python + FastAPI Setup (Recommended for ease of learning)

### Prerequisites
- **Python 3.9+** - [Download](https://www.python.org/)
- **pip** (comes with Python)

### 1. Navigate to Backend Directory
```bash
cd backend
```

### 2. Create Virtual Environment
```bash
python -m venv venv

# Activate
# Windows:
venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate
```

### 3. Install Dependencies
```bash
pip install fastapi uvicorn sqlalchemy psycopg2-binary python-dotenv pydantic pyjwt bcrypt
pip install -r requirements.txt
```

### 4. Set Up Environment Variables
Create `.env` file in `backend/`:

```
DATABASE_URL=postgresql://postgres:postgres@localhost:5432/micro_learning
SECRET_KEY=your-super-secret-key-change-this
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=30
PORT=3000
CORS_ORIGIN=http://localhost:4200
```

### 5. Start PostgreSQL with Docker
```bash
docker run --name postgres -e POSTGRES_PASSWORD=postgres -p 5432:5432 -d postgres:15

# Create database
docker exec -it postgres psql -U postgres -c "CREATE DATABASE micro_learning;"
```

### 6. Create Database Schema
```bash
# Create alembic migrations (if using)
alembic init migrations

# Run migrations
alembic upgrade head
```

### 7. Start Development Server
```bash
uvicorn main:app --reload --port 3000
```

Server runs at `http://localhost:3000`

### FastAPI Project Structure
```
backend/
├── main.py                    # Entry point
├── app/
│   ├── api/
│   │   ├── v1/
│   │   │   ├── __init__.py
│   │   │   ├── endpoints/
│   │   │   │   ├── auth.py
│   │   │   │   ├── lessons.py
│   │   │   │   ├── users.py
│   │   │   │   └── content.py
│   │   │   └── dependencies.py
│   │   └── router.py
│   ├── models/                # SQLAlchemy models
│   │   ├── __init__.py
│   │   ├── user.py
│   │   ├── lesson.py
│   │   └── content.py
│   ├── schemas/               # Pydantic schemas
│   │   ├── __init__.py
│   │   ├── user.py
│   │   └── lesson.py
│   ├── crud/                  # Database operations
│   │   ├── __init__.py
│   │   ├── user.py
│   │   └── lesson.py
│   ├── core/
│   │   ├── config.py
│   │   ├── security.py
│   │   └── __init__.py
│   ├── db/
│   │   ├── __init__.py
│   │   ├── base.py
│   │   └── session.py
│   └── __init__.py
├── migrations/                # Alembic migrations
├── tests/
│   ├── __init__.py
│   ├── conftest.py
│   ├── test_api.py
│   └── test_auth.py
├── requirements.txt
├── .env
├── .env.example
├── docker-compose.yml
└── Dockerfile
```

### Key FastAPI Commands
```bash
# Run with auto-reload (development)
uvicorn main:app --reload --port 3000

# Run with hot reload
uvicorn main:app --reload --host 0.0.0.0 --port 3000

# Generate OpenAPI docs
# Automatically available at http://localhost:3000/docs

# Run tests
pytest

# Run with coverage
pytest --cov=app
```

### FastAPI Example Endpoint
```python
from fastapi import FastAPI, HTTPException, Depends
from sqlalchemy.orm import Session
from app.schemas import LessonCreate, LessonResponse
from app.crud import create_lesson, get_lessons

app = FastAPI()

@app.post("/api/v1/lessons", response_model=LessonResponse)
async def create_lesson_endpoint(
    lesson: LessonCreate,
    db: Session = Depends(get_db)
):
    return create_lesson(db, lesson)

@app.get("/api/v1/lessons")
async def list_lessons(db: Session = Depends(get_db)):
    return get_lessons(db)
```

---

## Option 2: Java + Spring Boot Setup (Enterprise choice)

### Prerequisites
- **Java 17+** - [Download](https://adoptium.net/)
- **Maven 3.8+** or **Gradle 7+** - [Download](https://maven.apache.org/)
- **IDE**: IntelliJ IDEA or Eclipse

### 1. Create Spring Boot Project

**Using Spring Initializr** (recommended):
1. Go to [start.spring.io](https://start.spring.io)
2. Configure project:
   - Project: Maven
   - Language: Java
   - Spring Boot: 3.1.x
   - Project Metadata:
     - Group: `com.microlearning`
     - Artifact: `api`
     - Name: `Micro-Learning API`
3. Add dependencies:
   - Spring Web
   - Spring Data JPA
   - PostgreSQL Driver
   - Spring Security
   - JWT (jjwt)
   - Lombok
   - Spring Boot DevTools
4. Click Generate and extract

**OR via Maven CLI**:
```bash
mvn archetype:generate \
  -DgroupId=com.microlearning \
  -DartifactId=api \
  -DarchetypeArtifactId=maven-archetype-quickstart \
  -DinteractiveMode=false
```

### 2. Navigate to Backend Directory
```bash
cd backend
```

### 3. Configure Application Properties
Create `src/main/resources/application.yml`:

```yaml
spring:
  application:
    name: micro-learning-api
  
  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
    properties:
      hibernate:
        dialect: org.hibernate.dialect.PostgreSQLDialect
  
  datasource:
    url: jdbc:postgresql://localhost:5432/micro_learning
    username: postgres
    password: postgres
    driver-class-name: org.postgresql.Driver

  servlet:
    multipart:
      max-file-size: 10MB
      max-request-size: 10MB

server:
  port: 3000
  servlet:
    context-path: /api/v1

jwt:
  secret: your-super-secret-jwt-key-change-this
  expiration: 604800000  # 7 days in milliseconds

cors:
  allowed-origins: http://localhost:4200
```

### 4. Start PostgreSQL with Docker
```bash
docker run --name postgres -e POSTGRES_PASSWORD=postgres -p 5432:5432 -d postgres:15

# Create database
docker exec -it postgres psql -U postgres -c "CREATE DATABASE micro_learning;"
```

### 5. Start Development Server
```bash
# Using Maven
mvn spring-boot:run

# OR using IDE (Run Application.java)
```

Server runs at `http://localhost:3000/api/v1`

### Spring Boot Project Structure
```
backend/
├── src/
│   ├── main/
│   │   ├── java/com/microlearning/
│   │   │   ├── api/
│   │   │   │   ├── controller/
│   │   │   │   │   ├── AuthController.java
│   │   │   │   │   ├── LessonController.java
│   │   │   │   │   └── UserController.java
│   │   │   │   ├── model/
│   │   │   │   │   ├── User.java
│   │   │   │   │   ├── Lesson.java
│   │   │   │   │   └── Content.java
│   │   │   │   ├── dto/
│   │   │   │   │   ├── UserDTO.java
│   │   │   │   │   └── LessonDTO.java
│   │   │   │   ├── service/
│   │   │   │   │   ├── UserService.java
│   │   │   │   │   └── LessonService.java
│   │   │   │   ├── repository/
│   │   │   │   │   ├── UserRepository.java
│   │   │   │   │   └── LessonRepository.java
│   │   │   │   ├── security/
│   │   │   │   │   ├── JwtUtil.java
│   │   │   │   │   └── SecurityConfig.java
│   │   │   │   ├── exception/
│   │   │   │   │   └── GlobalExceptionHandler.java
│   │   │   │   └── Application.java
│   │   ├── resources/
│   │   │   ├── application.yml
│   │   │   └── application-prod.yml
│   └── test/
│       └── java/com/microlearning/api/
│           └── ApiApplicationTests.java
├── pom.xml
├── Dockerfile
└── docker-compose.yml
```

### Key Spring Boot Commands
```bash
# Run development server
mvn spring-boot:run

# Build JAR
mvn clean package

# Run tests
mvn test

# Run with specific profile
mvn spring-boot:run -Dspring-boot.run.profiles=dev
```

### Spring Boot Example Endpoint
```java
@RestController
@RequestMapping("/lessons")
@CrossOrigin(origins = "http://localhost:4200")
public class LessonController {
  
  @Autowired
  private LessonService lessonService;
  
  @GetMapping
  public ResponseEntity<List<LessonDTO>> getAllLessons() {
    return ResponseEntity.ok(lessonService.getAllLessons());
  }
  
  @PostMapping
  public ResponseEntity<LessonDTO> createLesson(@RequestBody LessonDTO lessonDTO) {
    return ResponseEntity.status(HttpStatus.CREATED)
      .body(lessonService.createLesson(lessonDTO));
  }
  
  @GetMapping("/{id}")
  public ResponseEntity<LessonDTO> getLesson(@PathVariable String id) {
    return ResponseEntity.ok(lessonService.getLesson(id));
  }
}
```

---

## Common Tasks (Both Options)

### Run Tests
**FastAPI:**
```bash
pytest
pytest --cov=app
```

**Spring Boot:**
```bash
mvn test
```

### Build Docker Image
```bash
docker build -t micro-learning-api .
docker run -p 3000:3000 --env-file .env micro-learning-api
```

### Database Migrations
**FastAPI (Alembic):**
```bash
alembic revision --autogenerate -m "Add new table"
alembic upgrade head
```

**Spring Boot (Flyway):**
- Add SQL migration files to `src/main/resources/db/migration/`
- Spring Boot auto-runs on startup

### Connect to Production Database
```bash
psql -h your-rds-endpoint.amazonaws.com -U postgres -d micro_learning
```

---

## Troubleshooting

### Python/FastAPI Issues

**Module not found:**
```bash
# Ensure virtual environment is activated
source venv/bin/activate  # or venv\Scripts\activate on Windows
pip install -r requirements.txt
```

**Port 3000 already in use:**
```bash
uvicorn main:app --reload --port 3001
```

### Java/Spring Boot Issues

**Port 3000 already in use:**
Update `application.yml`:
```yaml
server:
  port: 3001
```

**Build fails:**
```bash
mvn clean install
```

---

## Deployment

See [DEPLOYMENT.md](DEPLOYMENT.md) for AWS deployment instructions for both FastAPI and Spring Boot.

**Need help?** Create an issue or discussion on GitHub!
