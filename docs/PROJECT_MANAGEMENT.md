# Project Management Guide

How to run the 10-day hackathon smoothly using GitHub and open-source project management tools.

## 🎯 Philosophy

- **No external tools** - GitHub is your one source of truth
- **Clear ownership** - Everyone knows what they're working on
- **Transparent progress** - All decisions and discussions are visible
- **Inclusive** - New contributors can find work easily

---

## 1. GitHub Organization Setup

### Repository Permissions

- **Maintainers** (2-3 people): Can merge PRs, manage issues
- **Developers** (14 students): Can create branches, submit PRs
- **Everyone**: Can create discussions

### Branch Protection Rules

1. Go to Settings → Branches
2. Add rule for `main`:
   - ✅ Require a pull request review (1 approval minimum)
   - ✅ Dismiss stale pull request approvals
   - ✅ Require status checks to pass (CI/CD)
   - ✅ Require branches to be up to date

---

## 2. Using GitHub Issues

### Creating Issues

Every task should be an issue. Use this template:

```markdown
## Title
Clear, actionable title (e.g., "Add user authentication API")

## Description
- What needs to be done?
- Why is it needed?
- Any context or links?

## Acceptance Criteria
- [ ] Feature implemented
- [ ] Tests written
- [ ] Documentation updated
- [ ] No breaking changes

## Type
- [ ] Feature
- [ ] Bug
- [ ] Documentation
- [ ] Refactor

## Assignee
Assign to yourself when starting work
```

### Labels

Create these labels for categorization:

| Label | Color | Usage |
|-------|-------|-------|
| `feature` | Green | New features |
| `bug` | Red | Bug fixes |
| `documentation` | Blue | Documentation |
| `good first issue` | Purple | Good for newcomers |
| `help wanted` | Orange | Need help |
| `high priority` | Red | Urgent |
| `frontend` | Blue | Frontend work |
| `backend` | Purple | Backend work |
| `devops` | Yellow | DevOps/CI-CD |

### Milestones

Create milestones for each day:

```
Day 1-2: Architecture & Setup
Day 3-5: Core Development
Day 6-8: Features & Testing
Day 9: Polish
Day 10: Deployment & Demo
```

Assign issues to appropriate milestones.

---

## 3. Using GitHub Discussions

### Discussion Categories

Create these categories:

#### 🏗️ Architecture
- System design decisions
- Technology choices
- API design discussions

#### 🔧 Technical Help
- How-to questions
- Debugging help
- Library recommendations

#### 📝 Project Updates
- Daily standups
- Weekly summaries
- Announcements

#### 🎓 Learning
- Resources
- Best practices
- Code review discussions

### Daily Standup Template

Create a new discussion each day:

```markdown
# Day 3 Standup - February 11

## What we accomplished yesterday
- [x] User auth API completed
- [x] Frontend login page designed

## What we're working on today
- [ ] Implement lesson creation API
- [ ] Build lesson editor UI
- [ ] Write database migration

## Blockers
- PostgreSQL connection issues (being resolved)

## Celebrating
🎉 First PR merged! Thanks @student-name

## Open questions
- Should we use pagination or infinite scroll?
- Best approach for media uploads?
```

---

## 4. GitHub Projects (Kanban Board)

### Setup

1. Go to Projects → New
2. Create a table view with columns:
   - **Backlog** - Not started
   - **Ready** - Ready to work on
   - **In Progress** - Currently being worked on
   - **Review** - PR open, waiting for review
   - **Done** - Completed and merged

### Using the Board

1. Create issue
2. Add to project
3. Move through columns as work progresses
4. Auto-link to PRs

### Example Board

```
BACKLOG                IN PROGRESS              REVIEW                 DONE
├─ Design DB schema   ├─ Auth API              ├─ Login UI PR (#23)   ├─ Project setup
├─ API specs          ├─ Frontend layout       ├─ Lesson API PR (#24) ├─ Repository setup
├─ UI mockups         ├─ Docker setup          └─ Tests PR (#25)      └─ CI/CD configured
└─ ...                └─ ...                                          
```

---

## 5. Pull Request Workflow

### Creating a PR

```markdown
## Description
Implement user authentication with JWT tokens

## Type of Change
- [x] New feature
- [ ] Bug fix
- [ ] Documentation update

## Related Issue
Closes #42

## Changes Made
- Added POST /auth/register endpoint
- Added POST /auth/login endpoint
- Implemented JWT token generation
- Added password hashing with bcrypt

## Testing
- Tested with Postman
- All unit tests passing
- No breaking changes

## Checklist
- [x] Code follows style guide
- [x] Self-reviewed my code
- [x] Added tests
- [x] Updated documentation
- [x] No new warnings generated

## Screenshots (if UI changes)
[screenshots here]
```

### PR Review Checklist

When reviewing PRs:

- ✅ Does it solve the issue?
- ✅ Is code readable and maintainable?
- ✅ Are tests included?
- ✅ Does it break existing functionality?
- ✅ Are there security concerns?
- ✅ Is documentation updated?
- ✅ Are variable names clear?

### Merging PRs

- Require 1 approval minimum
- All status checks must pass (CI/CD)
- Delete branch after merging
- Celebrate! 🎉

---

## 6. Communication Strategy

### Real-time Chat (Slack/Discord - Optional but Recommended)

For quick questions and coordination. BUT:
- Final decisions should be in GitHub Discussions
- Refer back to GitHub for context
- Archive important messages in Discussions

### Channels

```
#general           - Announcements, fun stuff
#help              - Questions, blockers
#frontend          - Frontend team
#backend           - Backend team
#devops            - Deployment, CI/CD
#random            - Off-topic chat
```

### Daily Standup Schedule

- **Time**: 9:00 AM (or start of day)
- **Format**: Either:
  - 10-minute verbal standup in video call
  - Written standup in GitHub Discussions
- **Agenda**:
  - What did you do?
  - What are you doing today?
  - Any blockers?

---

## 7. Conflict Resolution

### If students need the same file

1. **Communicate in issue** - Discuss in the issue before starting
2. **Pair program** - Work together on complex features
3. **Feature branches** - Keep branches focused and small
4. **Frequent merges** - Merge to main regularly (multiple times per day)

### If merge conflicts occur

```bash
git fetch origin
git rebase origin/main
# Resolve conflicts
git add .
git rebase --continue
git push -f origin feature/name
```

---

## 8. Weekly Review Cycle

### End of Day (5 PM)

- All work pushed to GitHub
- PRs submitted or marked as WIP
- Issues updated with progress

### End of Each Day Ritual

- Check GitHub board
- Ensure issues are up-to-date
- Plan next day's work

### Mid-Point Review (Day 5)

- Demo what you've built
- Review GitHub board
- Adjust timeline if needed
- Celebrate progress

### Final Review (Day 10)

- All code merged to main
- Deployment complete
- Final demo ready

---

## 9. Documentation Standards

### Every Feature Should Have

1. **Issue** - Why this feature exists
2. **PR** - How it was implemented
3. **Code comments** - Complex logic explained
4. **README update** - How to use it
5. **API docs** - Endpoints documented (backend)

### GitHub Wiki (Optional)

Create a wiki for:
- System architecture diagrams
- Database schema
- Deployment runbooks
- Troubleshooting guide

---

## 10. Continuous Integration

### Every Push Triggers

1. Code linting
2. Run tests
3. Build project
4. Security scan (optional)

### Status Badge in README

```markdown
![CI/CD Status](https://github.com/YOUR-ORG/micro-learning-app/workflows/CI%2FCD/badge.svg)
```

---

## 11. Managing Technical Debt

### Don't Ignore It

Create issues for:
- Performance improvements
- Code refactoring
- Documentation gaps
- Test coverage

### Label as "technical-debt"

Review every Friday and tackle some during Day 9.

---

## 12. Sample Project Timeline

### Day 1: Setup (Architecture)
```
ISSUES:
├─ #1: Setup GitHub repo
├─ #2: Initialize frontend project (Vite + React)
├─ #3: Initialize backend project (Node.js + Express)
├─ #4: Setup PostgreSQL database
├─ #5: Create API specification
├─ #6: Design database schema
├─ #7: Setup CI/CD pipeline
└─ #8: Docker configuration

BOARD STATUS:
- DONE: 5-8 issues
- IN_PROGRESS: 1-4 issues
```

### Day 3-5: Development Sprint
```
ISSUES:
├─ #20: Implement auth endpoints
├─ #21: Build login UI
├─ #22: Setup authentication in frontend
├─ #23: Create lesson CRUD APIs
├─ #24: Build lesson editor
└─ ...

BOARD STATUS:
- DONE: Growing daily
- IN_PROGRESS: 3-4 per developer
- REVIEW: 2-3 PRs waiting
```

### Day 10: Launch
```
All issues in DONE
PRs merged to main
Production deployment complete
Demo ready!
```

---

## 13. Success Metrics

Track these metrics throughout the hackathon:

| Metric | Day 1 | Day 5 | Day 10 |
|--------|-------|-------|--------|
| Issues Created | 50+ | 100+ | 150+ |
| PRs Merged | 0 | 30+ | 80+ |
| Code Coverage | 0% | 40%+ | 70%+ |
| Bugs Fixed | 0 | 10+ | 20+ |
| Features Complete | 0% | 50% | 100% |

---

## Bonus: GitHub Resources for Students

- **GitHub Skills**: https://skills.github.com
- **GitHub Learning**: https://docs.github.com
- **First Contributions**: https://firstcontributions.github.io
- **Pro Tips**: Follow @github on Twitter

---

**Last Updated:** February 8, 2026
