# GitHub Discussions Template

This file documents the discussion categories and templates for team communication.

---

## Discussion Categories

Create these four categories in GitHub Discussions (Settings → Features → Set up discussions):

### 1. 📢 Announcements
For project-wide announcements, milestones, and important updates.

**Use for:**
- Release announcements
- Deadline reminders
- Milestone completions
- Team celebrations

### 2. 🗳️ Decisions  
For architectural decisions, tech stack votes, and process changes.

**Use for:**
- Backend framework vote (Python FastAPI vs Java Spring Boot)
- CI/CD tool selection (GitHub Actions vs Jenkins)
- Architecture design discussions
- Process improvements

### 3. 🆘 Help & Questions
For Q&A, debugging help, and how-to discussions.

**Use for:**
- Setup questions
- Debugging issues
- "How do I...?" questions
- Library/tool recommendations

### 4. 📚 General
For off-topic chat, learning resources, and project learnings.

**Use for:**
- Sharing learning resources
- Best practice discussions
- Code review tips
- Team learnings and retrospectives

---

## Daily Standup Template

Create a new discussion each day using this template:

```markdown
# Day X Standup - [Date]

## ✅ What We Completed Yesterday
- [ ] Item 1
- [ ] Item 2
- [ ] Item 3

## 🔧 What We're Working On Today
- [ ] Priority item 1
- [ ] Priority item 2
- [ ] Priority item 3

## 🚧 Blockers
- Blocker 1 (assigned to: @username)
- Blocker 2 (assigned to: @username)

## 🎉 Celebrating
- First PR merged! 🎉 @student-name
- Feature complete! ✨ @student-name

## ❓ Open Questions
- Question 1?
- Question 2?
```

---

## Tech Stack Vote Template

Use this for the backend and CI/CD framework vote:

```markdown
# 🗳️ Tech Stack Decision: [Option A] vs [Option B]

## Summary
We need to decide between Option A and Option B for [feature/component].

## Option A: [Name]
**Pros:**
- Pro 1
- Pro 2
- Pro 3

**Cons:**
- Con 1
- Con 2

**Setup Time:** X minutes  
**Best For:** [Use case]

**Vote:** React with 👍

---

## Option B: [Name]
**Pros:**
- Pro 1
- Pro 2
- Pro 3

**Cons:**
- Con 1
- Con 2

**Setup Time:** X minutes  
**Best For:** [Use case]

**Vote:** React with 👎

---

## Discussion
Reply with your preference and reasoning!

---

**Voting closes:** [Date & Time]  
**Decision announced:** [Date & Time]
```

---

## Architecture Design Discussion Template

```markdown
# 🏗️ Architecture Discussion: [Component Name]

## Current Challenge
[Describe what problem we're solving]

## Proposed Solution
[Describe your proposal with diagram or pseudocode if helpful]

## Pros
- Benefit 1
- Benefit 2

## Cons  
- Risk/drawback 1
- Risk/drawback 2

## Alternatives Considered
- Alternative 1: [Brief description]
- Alternative 2: [Brief description]

## Questions
- Question 1?
- Question 2?

**Next Steps:**  
Decision by: [date]
```

---

## How to Use Discussions

### Posting a Comment
- Click "Reply" to respond
- Keep comments focused and constructive
- Link to related issues with `#issue-number`
- Link to related PRs with `#pr-number`

### Using Reactions
- 👍 = Yes / Agree
- 👎 = No / Disagree  
- ❤️ = Love it
- 🎉 = Celebration
- 😕 = Confused
- 🚀 = Prioritize this
- 📌 = Important

### Marking as Answered
Once a question is resolved:
1. Reply with the solution
2. Click "Mark as Answer" on the best reply
3. Close the discussion if completely resolved

---

## Important Notes

**DO:**
- Use GitHub Discussions for all project decisions (keeps things searchable and documented)
- Link issues and PRs in discussions
- Reference discussions in commit messages when relevant
- Keep discussions organized by category

**DON'T:**
- Use Google Chat for important project decisions (not searchable, not documented)
- Post sensitive information (secrets, passwords, personal data)
- Spam or off-topic content (use #general in Google Chat instead)

---

## Integration with Google Chat

- Important announcements → Google Chat first, then GitHub Discussions
- Questions → Always ask in GitHub Discussions (searchable for future students)
- Quick questions → Google Chat is fine
- Architecture/decisions → ALWAYS GitHub Discussions

---

**Remember:** Good documentation means future students can learn from your discussions!
