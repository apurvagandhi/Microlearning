# Contributing to Micro-Learning App

Thank you for contributing to this open-source project! This guide will help you get started.

## ⚠️ Important: Our Tech Stack is Still Being Decided!

We're using **placeholder technologies** right now while we decide as a team:

- **Frontend**: Placeholder is **Angular** (alternatives: React, Vue.js)
- **Backend**: Placeholder is **Java + Spring Boot** (alternatives: Python + FastAPI, Node.js)
- **Deployment**: Placeholder is **AWS** (with decisions on Jenkins vs GitHub Actions)

**Your team will vote and decide on final tech stack through GitHub Discussions!** See [docs/GITHUB_GUIDE.md](docs/GITHUB_GUIDE.md) for more details.

All setup guides and documentation will be updated once decisions are made.

---

## 🚀 Getting Started

### Prerequisites
- Git installed
- **Frontend**: Node.js 18+ (for Angular)
- **Backend**: Java 17+ OR Python 3.9+ (depending on your track and final decision)
- GitHub account
- Read [docs/GITHUB_GUIDE.md](docs/GITHUB_GUIDE.md) to understand our GitHub workflow ⭐

### Initial Setup

1. **Fork and clone the repository**
   ```bash
   git clone https://github.com/YOUR-USERNAME/micro-learning-app.git
   cd micro-learning-app
   ```

2. **Add upstream remote**
   ```bash
   git remote add upstream https://github.com/ORIGINAL-OWNER/micro-learning-app.git
   ```

3. **Follow environment setup**
   - **Frontend (Angular)**: See [docs/FRONTEND_SETUP.md](docs/FRONTEND_SETUP.md)
   - **Backend (Java/Python)**: See [docs/BACKEND_SETUP.md](docs/BACKEND_SETUP.md)
   - **GitHub Workflow**: See [docs/GITHUB_GUIDE.md](docs/GITHUB_GUIDE.md)

---

## 📋 Workflow

### 1. Understand Our GitHub Process

Before contributing, please read **[docs/GITHUB_GUIDE.md](docs/GITHUB_GUIDE.md)**. It explains:
- How code review works (CODEOWNERS)
- How to write good issues
- How to write good PRs
- Why we have these processes

**New to GitHub?** Start there! 📚

### 2. Find or Create an Issue
- Browse [GitHub Issues](../../issues)
- Filter by `good first issue` or `help wanted`
- If you found a bug or have a feature idea, **create an issue first** using our templates
- Describe the problem/feature clearly with context
- Check our [issue templates](/.github/ISSUE_TEMPLATE/) for how to write good issues

### 3. Assign Yourself
- Comment on the issue: "I'd like to work on this!"
- Wait for acknowledgment (or just start if it's a `good first issue`)
- Assign yourself to the issue

### 4. Create a Feature Branch
```bash
# Keep main branch clean
git checkout main
git pull upstream main

# Create feature branch with descriptive name
git checkout -b feature/issue-123-add-auth
# or
git checkout -b bugfix/issue-456-fix-login
# or
git checkout -b docs/issue-789-api-guide
```

**Branch naming convention:**
- `feature/issue-NUMBER-short-description` - new features
- `bugfix/issue-NUMBER-short-description` - bug fixes
- `docs/issue-NUMBER-short-description` - documentation
- `refactor/issue-NUMBER-short-description` - code improvements

### 5. Make Your Changes

#### Commit Best Practices
```bash
# Make logical, focused commits (one thing per commit)
git commit -m "feat: add user authentication endpoint

- Implement JWT token generation
- Add password hashing with bcrypt
- Create /auth/login endpoint
Closes #123"
```

**Commit message format:**
```
<type>: <subject>

<body>

<footer>
```

**Types:** 
- `feat` - new feature
- `fix` - bug fix
- `docs` - documentation changes
- `style` - formatting, linting (no code change)
- `refactor` - code restructuring (no behavior change)
- `test` - adding/updating tests
- `chore` - build, deps, config changes

**Tips:**
- Keep commits focused on one thing
- Write clear commit messages (future you will thank you!)
- Link to the issue: `Closes #123`

### 6. Push and Create a Pull Request

```bash
git push origin feature/issue-123-add-auth
```

Then on GitHub:
1. Go to the repository and create a Pull Request
2. **The PR template will appear automatically** - don't skip it!
3. Fill in:
   - **Title**: Clear, concise description
   - **Description**: What changes? Why? How to test?
   - **Type of Change**: Bug fix? Feature? Docs?
   - **Related Issue**: `Closes #123`
   - **Testing**: How did you test it?
   - **Checklist**: Make sure all items are checked

**See [/.github/pull_request_template.md](/.github/pull_request_template.md) for the full template**

### 7. Code Review

**Important: Code review is a learning opportunity, not a judgment!**

- **Code owners will be automatically assigned** (see [/.github/CODEOWNERS](/.github/CODEOWNERS))
- Respond to feedback politely and thoughtfully
- Ask questions if you don't understand feedback
- Make requested changes and re-request review
- Once approved ✅, a maintainer will merge

**Tips:**
- Be open to suggestions
- Ask "Why?" if something seems wrong
- Learn from feedback
- Remember: everyone was a beginner once!

### 8. Cleanup

```bash
git checkout main
git pull upstream main
git branch -d feature/issue-123-add-auth
```

---

## 💻 Development Guidelines

### Code Style

**All code should be readable and maintainable.**

#### Frontend (Angular + TypeScript)
- Use **Prettier** for formatting: `npm run format`
- Follow **ESLint** rules: `npm run lint`
- Use TypeScript strictly (no `any` type unless absolutely necessary)
- Use components, services, and proper Angular patterns
- Write comments for complex logic

```bash
cd frontend
npm run lint      # Check for issues
npm run format    # Auto-format code
```

#### Backend (Java or Python)
- **Java**: Follow Google Java Style Guide
  - Use meaningful variable names
  - Write Javadoc comments for public methods
  - Run linting and formatting tools

- **Python**: Follow PEP 8 standard
  - Use `black` for formatting
  - Use `flake8` for linting
  - Write docstrings for functions

```bash
# Python
black .           # Format code
flake8 .          # Check for issues
```

### Testing

**Always write tests for new features!**

```bash
# Frontend - Angular
cd frontend
ng test           # Run unit tests

# Backend - Python
cd backend
python -m pytest  # Run tests
pytest --cov      # Check coverage
```

**Guidelines:**
- Test the happy path (when things work)
- Test edge cases (boundary conditions)
- Test error scenarios (what happens when things fail)
- Keep tests focused on one thing
- Use descriptive test names

### Documentation

**Good documentation helps everyone!**

- Update `README.md` if your change affects overall project
- Add inline comments for complex logic
- Update API docs if you change endpoints
- Update setup guides if you add new steps
- Add JSDoc comments (Frontend) or Docstrings (Backend)

Example JSDoc (Frontend):
```typescript
/**
 * Authenticates a user with email and password
 * @param email - User's email address
 * @param password - User's password
 * @returns Promise<UserToken> - JWT token if successful
 * @throws AuthenticationError - If credentials are invalid
 */
login(email: string, password: string): Promise<UserToken> {
  // implementation
}
```

Example Docstring (Python):
```python
def authenticate_user(email: str, password: str) -> dict:
    """
    Authenticate a user with email and password.
    
    Args:
        email: User's email address
        password: User's password
    
    Returns:
        dict: Contains JWT token if successful
    
    Raises:
        AuthenticationError: If credentials are invalid
    """
    # implementation
```

---

## 📝 Common Issues & Solutions

### "I want to contribute but don't know where to start"
→ Look for issues labeled `good first issue`
→ Read [docs/GITHUB_GUIDE.md](docs/GITHUB_GUIDE.md)
→ Ask questions in GitHub Discussions!

### "My PR is being blocked by code review"
→ This is normal! Review is about learning and quality
→ Read the feedback carefully
→ Ask for clarification if needed
→ Make the requested changes
→ Push again and re-request review

### "I'm confused about the tech stack"
→ It's a placeholder right now!
→ Check [readme.md](readme.md) for current info
→ The team will vote on final stack soon
→ Setup guides will be updated accordingly

### "I made a mistake in my commit"
→ Don't worry, it happens to everyone!
→ Use `git commit --amend` to fix the last commit
→ Use `git revert` if changes are already merged
→ Ask for help if unsure!

### "Tests are failing"
→ Run tests locally first: `npm run test` or `pytest`
→ Check the error message carefully
→ Ask the team in Slack for help
→ All tests must pass before PR can be merged

---

## 🐛 Reporting Bugs

Use the [bug report template](/.github/ISSUE_TEMPLATE/bug_report.md) to create an issue with:

- **Title**: Clear bug description
- **Environment**: OS, browser, Node version, etc.
- **Steps to reproduce**: Exact steps to trigger the bug
- **Expected vs actual behavior**
- **Screenshots/error logs**

Example:
```markdown
## [BUG] Login button unresponsive on mobile

**Environment:** 
- OS: iOS 15.2
- Browser: Safari
- Node: 18.0.0

**Steps to reproduce:**
1. Navigate to login page on iPhone
2. Enter email and password
3. Click login button

**Expected:** User logs in and redirects to dashboard
**Actual:** Nothing happens

**Error Log:** 
```
XMLHttpRequest error: POST /auth/login 500
```

**Screenshots:** [attach screenshot]
```

---

## 💡 Feature Requests

Use the [feature request template](/.github/ISSUE_TEMPLATE/feature_request.md) to create an issue with:

- **Title**: Feature description
- **Use case**: Why is this needed?
- **Proposed solution**: How would you implement it?
- **Acceptance criteria**: What needs to be true for this to be complete?
- **Alternatives considered**: Other approaches?

---

## 🚨 Code Review Tips

### When Your PR is Being Reviewed:
- ✅ Don't take feedback personally - it's about the code!
- ✅ Respond to all comments
- ✅ Ask questions if feedback is unclear
- ✅ Thank reviewers for their time and feedback
- ✅ Make changes and re-request review

### When You're Reviewing Someone Else's PR:
- ✅ Be kind and constructive
- ✅ Praise good code and approaches
- ✅ Ask questions instead of making demands
- ✅ Suggest improvements, don't demand them
- ✅ Test the code if possible
- ✅ Focus on code quality, not personal style

### Code Review Checklist:
- ✅ Does it solve the issue or implement the feature?
- ✅ Is the code readable and maintainable?
- ✅ Are there tests? Do they pass?
- ✅ Does it break any existing functionality?
- ✅ Is documentation updated?
- ✅ Are there security or performance concerns?
- ✅ Does it follow our code style and patterns?

---

## 📚 Resources

- **GitHub Guide**: [docs/GITHUB_GUIDE.md](docs/GITHUB_GUIDE.md) ⭐
- **Frontend Setup**: [docs/FRONTEND_SETUP.md](docs/FRONTEND_SETUP.md)
- **Backend Setup**: [docs/BACKEND_SETUP.md](docs/BACKEND_SETUP.md)
- **Architecture**: [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)
- **API Reference**: [docs/API.md](docs/API.md)

**External Resources:**
- [GitHub Help](https://docs.github.com)
- [Git Guide](https://git-scm.com/book/en/v2)
- [Angular Docs](https://angular.io)
- [Java Spring Boot](https://spring.io/projects/spring-boot)
- [Python FastAPI](https://fastapi.tiangolo.com)
- [Conventional Commits](https://www.conventionalcommits.org/)

---

## ❓ Questions or Need Help?

- **Create a GitHub Issue** - Use our templates
- **GitHub Discussions** - Ask general questions
- **Code Review Comments** - Ask for clarification
- **Google Chat** - Chat with the team in real-time

---

## 🙌 Code of Conduct

We are committed to providing a welcoming and inclusive environment:

- **Be respectful** to all team members
- **Be helpful** and supportive
- **Be patient** - everyone is learning
- **Assume good intent** - ask clarifying questions
- **Report issues** to organizers if needed

---

## 🎉 Thank You!

**Thank you for contributing to the Micro-Learning App!** Your effort, creativity, and dedication help make this project better for everyone. Whether you write code, fix bugs, improve documentation, or suggest features - it all matters!

**We're all learning together. Enjoy the process!** 🚀
