# 🎓 NC State Micro-Learning App Hackathon - Setup Complete!

Welcome to the Micro-Learning App! This is your complete guide to a successful 10-day open-source hackathon.

---

## 📖 Quick Navigation

### For Students
1. **First Time Setup**: Read [docs/FRONTEND_SETUP.md](docs/FRONTEND_SETUP.md) or [docs/BACKEND_SETUP.md](docs/BACKEND_SETUP.md)
2. **How to Contribute**: Read [CONTRIBUTING.md](CONTRIBUTING.md)
3. **Understanding GitHub**: Read [docs/GITHUB_GUIDE.md](docs/GITHUB_GUIDE.md) ⭐ **Start here if new to GitHub!**
4. **Find Work to Do**: Check [GitHub Issues](../../issues) - Look for `good first issue`
5. **Understand the Project**: Check [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)

### For Project Managers
1. **Project Management**: Read [docs/PROJECT_MANAGEMENT.md](docs/PROJECT_MANAGEMENT.md)
2. **Daily Checklist**: Use [docs/HACKATHON_CHECKLIST.md](docs/HACKATHON_CHECKLIST.md)
3. **External Setup**: [docs/EXTERNAL_SETUP.md](docs/EXTERNAL_SETUP.md)
4. **Track Progress**: Use [GitHub Projects Board](../../projects)

### For Technical Leads
1. **API Design**: [docs/API.md](docs/API.md)
2. **Architecture**: [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)
3. **Deployment**: [docs/DEPLOYMENT.md](docs/DEPLOYMENT.md)
4. **Code Standards**: [CONTRIBUTING.md](CONTRIBUTING.md#code-standards)

---

## 🚀 Getting Started in 5 Minutes

### 1. Clone the Repository
```bash
git clone https://github.com/YOUR-ORG/micro-learning-app.git
cd micro-learning-app
```

### 2. Pick Your Track

#### Frontend Track (Angular)
```bash
cd frontend
npm install
ng serve
# Visit http://localhost:4200
```

#### Backend Track (Python/Java - TBD)
```bash
cd backend

# If Python + FastAPI is chosen:
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows
pip install -r requirements.txt
uvicorn main:app --reload
# Visit http://localhost:3000

# If Java + Spring Boot is chosen:
mvn spring-boot:run
# Visit http://localhost:3000/api/v1
```

> **Note:** Backend framework to be decided Tuesday. See [ORGANIZER_NOTES.md](ORGANIZER_NOTES.md) for voting details.

### 3. Find an Issue
- Go to [GitHub Issues](../../issues)
- Filter by `good first issue`
- Comment: "I'd like to work on this"
- Assign yourself

### 4. Create a Branch
```bash
git checkout -b feature/issue-123-short-name
```

### 5. Make Changes & Push
```bash
git add .
git commit -m "feat: short description

- More details
- Closes #123"
git push origin feature/issue-123-short-name
```

### 6. Create Pull Request
- Go to repository
- Create PR
- Add description and link issue
- Wait for review
- Merge when approved!

---

## 📚 Essential Documentation

| Document | Purpose | For Whom |
|----------|---------|----------|
| [README.md](README.md) | Project overview | Everyone |
| [CONTRIBUTING.md](CONTRIBUTING.md) | How to contribute | All developers |
| [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) | System design & decisions | Tech leads, senior devs |
| [docs/FRONTEND_SETUP.md](docs/FRONTEND_SETUP.md) | Frontend dev environment | Frontend developers |
| [docs/BACKEND_SETUP.md](docs/BACKEND_SETUP.md) | Backend dev environment | Backend developers |
| [docs/API.md](docs/API.md) | Complete API reference | Full-stack, backend devs |
| [docs/DEPLOYMENT.md](docs/DEPLOYMENT.md) | How to deploy to production | DevOps leads |
| [docs/PROJECT_MANAGEMENT.md](docs/PROJECT_MANAGEMENT.md) | How to use GitHub effectively | Project managers, leads |
| [docs/EXTERNAL_SETUP.md](docs/EXTERNAL_SETUP.md) | External tools & accounts | Organizers |
| [docs/HACKATHON_CHECKLIST.md](docs/HACKATHON_CHECKLIST.md) | Day-by-day checklist | Project managers |

---

## 👥 Team Roles (Suggested)

Pick 14 students, organize into roles:

```
Frontend (4 students)
├─ Frontend Lead 1
├─ Frontend Lead 2
├─ Frontend Developer 1
└─ Frontend Developer 2

Backend (4 students)
├─ Backend Lead 1
├─ Backend Lead 2
├─ Backend Developer 1
└─ Backend Developer 2

DevOps & QA (3 students)
├─ DevOps Engineer
├─ QA Engineer 1
└─ QA Engineer 2

Design & Management (3 students)
├─ UI/UX Designer
├─ Technical Writer
└─ Project Manager
```

---

## 🗓️ 10-Day Timeline

### Day 1-2: Architecture & Setup
- Design system architecture
- Set up development environments
- Initialize projects
- Configure CI/CD pipeline
- Create GitHub issues

**Target**: All environments working, 50+ issues created

### Day 3-5: Core Development
- Implement authentication
- Build core APIs
- Create frontend layout
- Get frontend/backend talking

**Target**: 30+ PRs merged, core features working

### Day 6-8: Features & Testing
- Implement lesson management
- Add multi-modal content support
- Write tests
- Fix bugs

**Target**: 60+ PRs merged, core features complete

### Day 9: Polish & Optimization
- Code optimization
- Performance tuning
- UI/UX refinement
- Documentation updates

**Target**: All tests passing, no linting errors

### Day 10: Deployment & Demo
- Deploy to production
- Run final tests
- Prepare and deliver demo
- Celebrate! 🎉

**Target**: Production deployment complete, impressive demo

---

## 🛠️ Tech Stack

### Frontend
- **React 18** with Vite
- **TailwindCSS** for styling
- **Zustand** for state management
- **React Router** for navigation

### Backend
- **Node.js** + **Express.js**
- **PostgreSQL** for database
- **JWT** for authentication
- **Docker** for containerization

### DevOps
- **GitHub Actions** for CI/CD
- **Vercel** for frontend hosting
- **Railway** for backend hosting

---

## 📞 Communication

### Daily Standup
**Time**: 9:00 AM (or your start time)
**Location**: Video call or [GitHub Discussions](../../discussions)
**Format**:
- What did you do yesterday?
- What are you doing today?
- Any blockers?

### Getting Help
1. **Check documentation first** - Most answers are in docs/
2. **Search closed issues** - Someone probably had the issue
3. **Create a new issue** - If stuck, document it
4. **Ask in Slack/Discord** - For quick questions
5. **Start a discussion** - For architecture questions

### Reporting Progress
- Update GitHub issues regularly
- Move cards on [GitHub Projects](../../projects) board
- Comment on PRs with progress
- Celebrate wins in Slack! 🎉

---

## 🎯 Success Criteria

By the end of Day 10, you should have:

- ✅ 80+ PRs merged
- ✅ 120+ issues closed
- ✅ 70%+ code coverage
- ✅ All tests passing
- ✅ Frontend deployed to Vercel
- ✅ Backend deployed to Railway
- ✅ Working authentication
- ✅ Users can create and view lessons
- ✅ Multi-modal content support
- ✅ Progress tracking
- ✅ Complete documentation
- ✅ Impressive demo

---

## 🚨 Important Reminders

### ⚠️ DO NOT
- Commit `.env` files with secrets
- Commit `node_modules/` or `__pycache__/`
- Force push to `main` branch
- Merge without code review
- Skip writing tests
- Leave broken code in main

### ✅ DO
- Write clear commit messages
- Ask for help early
- Review others' PRs quickly
- Test your code locally first
- Update documentation
- Keep branches small and focused
- Communicate often

---

## 🎓 Learning Outcomes

After this hackathon, you'll understand:

1. **Open Source Development**
   - How to contribute to projects
   - Code review best practices
   - Collaborative development

2. **Full-Stack Development**
   - Frontend frameworks (React)
   - Backend APIs (Node.js)
   - Databases (PostgreSQL)

3. **DevOps & Deployment**
   - CI/CD pipelines
   - Docker containerization
   - Cloud deployment

4. **Project Management**
   - Using GitHub Issues effectively
   - Working in agile sprints
   - Team coordination

5. **Software Engineering**
   - Code quality
   - Testing practices
   - Documentation

---

## 📊 Track Your Progress

Check these metrics throughout the hackathon:

```
Day 1   |████░░░░░░░░░░░░░░░░ 20% - Architecture done
Day 3   |████████░░░░░░░░░░░░ 40% - Core APIs working
Day 5   |████████████░░░░░░░░ 60% - Features implemented
Day 8   |████████████████░░░░ 80% - Polishing
Day 10  |████████████████████ 100% - LAUNCHED! 🚀
```

---

## 🎉 Final Notes

This is a real open-source project. Everything you build will be:
- **Public** - Available on GitHub
- **Useful** - Actually helps people learn
- **Professional** - Follows industry standards
- **Educational** - You'll learn real skills

Be proud of your work!

---

## 🤝 Community

This project is open source. After the hackathon:
- Keep the repo public
- Accept contributions from others
- Share your experience
- Help future contributors
- Maybe it becomes a real tool!

---

## 📖 Next Steps

1. **Read** [CONTRIBUTING.md](CONTRIBUTING.md)
2. **Set up** your development environment
3. **Check** [GitHub Issues](../../issues) for first task
4. **Join** the daily standup
5. **Have fun** building!

---

**Ready to build something amazing?**

```
git clone https://github.com/YOUR-ORG/micro-learning-app.git
cd micro-learning-app
# Pick your track and start coding!
```

**Questions?** Create an issue or start a discussion.

**Let's go!** 🚀

---

**Last Updated:** February 8, 2026

**Built with ❤️ for NC State University Computer Science Students**
