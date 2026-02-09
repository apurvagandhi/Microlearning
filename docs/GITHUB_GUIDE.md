# 📂 GitHub Configuration Guide

This document explains the GitHub configuration files (`.github/` folder) and how they help manage our hackathon project.

---

## 🎓 What is the `.github/` Folder?

The `.github/` folder contains special GitHub configuration files that help manage your project:
- **Issue templates** - Guide people on how to report bugs/features
- **Pull request templates** - Guide people on how to submit code
- **Code owners** - Specify who should review what
- **Workflows** - Automate testing and deployment

---

## 📋 Files in Our Project

### 1. `.github/CODEOWNERS` - Code Review Automation

**What it does:**
- Automatically assigns reviewers when code is changed
- Ensures the right people review the right parts of the code
- Can block PRs if required reviewers haven't approved

**How it works:**
```
/frontend/ @frontend-lead-1 @frontend-lead-2
# This means: when code in /frontend/ changes, automatically request review from frontend leads
```

**For Students:**
- When you create a PR, GitHub automatically asks the code owners to review it
- This is normal and expected!
- Code owners have responsibility to review changes in their area
- Helps ensure code quality and knowledge sharing

**Example:**
You create a PR that modifies `frontend/src/app.component.ts`
→ GitHub automatically asks frontend leads to review
→ They check your code, ask questions, approve or request changes
→ Once approved, you can merge!

---

### 2. `.github/pull_request_template.md` - PR Structure Guide

**What it does:**
- Shows up automatically when you create a new PR
- Guides you on what information to include
- Makes reviews faster and more consistent

**Template includes:**
- ✅ Description of changes
- ✅ Type of change (bug fix, feature, etc.)
- ✅ How you tested it
- ✅ Checklist to ensure quality

**For Students:**
- Don't ignore this template! Fill it out!
- It takes 2 minutes but helps reviewers understand your changes faster
- Better PRs = faster approval = your code gets merged sooner!

**Example PR description:**
```
## Description
Fixed the login button not responding on mobile devices.

Fixes #42

## Type of Change
- [x] Bug fix

## How Has This Been Tested?
- Tested on iPhone 12 in Chrome
- Tested on Samsung Galaxy S21 in Chrome
- Tested on desktop (still works)
```

---

### 3. `.github/ISSUE_TEMPLATE/` - Issue Templates

The issue templates guide people on how to report bugs and suggest features.

#### Bug Report Template

**What it does:**
- Guides you on reporting bugs clearly
- Asks for steps to reproduce
- Asks for screenshots
- Helps developers fix bugs faster

**When to use:**
- Something is broken
- You found an error
- Feature doesn't work as expected

**Example:**
```
Title: [BUG] Login button not responding on mobile

Describe the Bug:
The login button doesn't work when I use my phone.

Steps to Reproduce:
1. Go to https://app.com
2. Tap the login button on your phone
3. Nothing happens

Expected: Login modal should open
Actual: Nothing happens
```

#### Feature Request Template

**What it does:**
- Guides you on suggesting new features
- Asks for the use case
- Asks for acceptance criteria
- Helps developers understand what you need

**When to use:**
- You want a new feature
- You have an idea to improve the app
- Something would be better if...

**Example:**
```
Title: [FEATURE] Dark mode support

Problem Statement:
My eyes hurt when using the app at night.

Proposed Solution:
Add a dark mode toggle in settings.

Acceptance Criteria:
- [ ] Toggle switch in settings
- [ ] All pages support dark mode
- [ ] Preference saved to user account
```

#### Documentation Update Template

**What it does:**
- Guides you on suggesting documentation improvements
- Points you to all the docs
- Makes documentation better for everyone

**When to use:**
- Documentation is confusing
- Instructions are outdated
- Something is missing
- You found a typo

---

## 🔄 How GitHub Configuration Works Together

Here's the typical flow:

### 1. **Finding Work**
```
Look at GitHub Issues
↓
See bug reports and feature requests
↓
Comment "I'll work on this!"
```

### 2. **Creating Your Branch**
```
git checkout -b fix/issue-123-short-name
↓
Make your changes
```

### 3. **Creating a Pull Request**
```
git push origin fix/issue-123-short-name
↓
Go to GitHub
↓
Click "Create Pull Request"
↓
PR Template appears automatically
↓
Fill it out with description and checklist
```

### 4. **Automatic Review Assignment**
```
You submit PR
↓
GitHub reads CODEOWNERS file
↓
Automatically requests review from code owners
↓
"frontend-lead-1 requested changes" appears
```

### 5. **Code Review & Approval**
```
Reviewers read your PR
↓
They test your code
↓
They ask questions or approve
↓
You make requested changes
↓
They approve
↓
You merge!
```

---

## 📖 Best Practices for Students

### When Creating Issues:

✅ **DO:**
- Be specific and clear
- Include steps to reproduce (for bugs)
- Add screenshots if possible
- Search for existing issues first
- Use the provided templates

❌ **DON'T:**
- Be vague: "Things are broken"
- Create duplicate issues
- Include sensitive information
- Create multiple issues for one problem

### When Creating PRs:

✅ **DO:**
- Use the PR template
- Link to the issue your fixing: "Fixes #123"
- Write a clear description
- Include how you tested it
- Keep PRs focused on one thing
- Ask for help if unsure

❌ **DON'T:**
- Skip the template
- Make huge changes in one PR
- Change unrelated things
- Leave TODO comments
- Merge your own PR without approval

### When Reviewing Code:

✅ **DO:**
- Be kind and constructive
- Suggest improvements, don't demand them
- Ask questions if unclear
- Test the code locally
- Approve when satisfied

❌ **DON'T:**
- Be harsh or rude
- Approve without reviewing
- Request changes on style preferences
- Block PRs for minor issues

---

## 🎯 Common Workflows

### "I found a bug!"

1. Go to Issues
2. Click "New Issue"
3. Select "Bug Report"
4. Fill out the template
5. Include steps to reproduce
6. Submit!

→ A developer will pick it up and fix it

### "I have an idea!"

1. Go to Issues
2. Click "New Issue"
3. Select "Feature Request"
4. Describe the use case
5. Suggest a solution
6. Submit!

→ The team will discuss and decide

### "I want to fix a bug!"

1. Find a bug issue
2. Comment: "I'll fix this!"
3. Create a branch: `git checkout -b fix/issue-123-description`
4. Make changes
5. Push: `git push origin fix/issue-123-description`
6. Create PR (template appears)
7. Fill out PR template completely
8. Wait for code owner review
9. Make changes if requested
10. Merge when approved!

### "The docs are confusing!"

1. Go to Issues
2. Click "New Issue"
3. Select "Documentation Update"
4. Point out what's confusing
5. Suggest improvements
6. Submit!

→ Docs team will update it

---

## 🤔 Frequently Asked Questions

### "Why am I getting automatic review requests?"

That's the CODEOWNERS file! It automatically assigns reviewers to make sure the right experts review your code. This is normal and good!

### "Can I merge my own PR?"

Generally no. You should get approval from a code owner first. This ensures:
- Code quality
- Knowledge sharing
- Catch potential issues early
- Learning from experienced developers

### "Why is my PR being blocked?"

GitHub might be preventing merge because:
- A code owner hasn't approved yet
- Tests are failing
- There are merge conflicts
- A checklist item isn't complete

All of these are helping you write better code!

### "How long does code review take?"

Usually 1-2 days during the hackathon. The team tries to review PRs quickly so you don't get blocked. If it's been 3+ days, ask on Slack!

### "What if I disagree with a review comment?"

That's okay! Open a discussion:
- Ask why they suggested it
- Explain your approach
- Work together to find the best solution
- This is how you learn!

---

## 📚 Learn More

- [GitHub Docs: Code Owners](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners)
- [GitHub Docs: Issue Templates](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/syntax-for-issue-forms)
- [GitHub Docs: Pull Request Templates](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/creating-a-pull-request-template-for-your-repository)
- [Conventional Commits](https://www.conventionalcommits.org/) - How to write good commit messages

---

## 🚀 Summary

| File | Purpose | For Whom |
|------|---------|----------|
| `CODEOWNERS` | Auto-assign code reviewers | Developers, Project Managers |
| `pull_request_template.md` | Guide for submitting code | All developers |
| `ISSUE_TEMPLATE/bug_report.md` | Guide for reporting bugs | All team members |
| `ISSUE_TEMPLATE/feature_request.md` | Guide for requesting features | All team members |
| `ISSUE_TEMPLATE/docs_update.md` | Guide for docs improvements | Documentation team |

These files make our project more organized and help everyone contribute effectively!

---

**Questions?** Ask on Slack or create a GitHub Discussion! 🎯
