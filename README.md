# CS-Learning-Log
## Part 1 — Git Basics
You learned that Git is **local**.

```text
Your Computer
     │
     ▼
Git Repository (.git)
```

It tracks every change in your project.

**Important commands:**

git init
Creates a Git repository.

git status
Shows changed files.

git add .
Stages files.

git commit -m "message"
Creates a snapshot of your project.

git remote add origin <repository-url>
After that:

```bash
git push
uploads your commits.

---

## Part 3 — Why Push Initially Failed

Your GitHub repository already had

```text
README.md
```

while your local repository had its own history.

Git protected both histories.

Solution:

```bash
git pull origin main --allow-unrelated-histories
```

Merge

↓

Commit merge

↓

Push again

↓

Success ✅

Now your local and GitHub repositories are synchronized.

---

## Part 4 — Authentication

You learned that Git Credential Manager is simply Git asking:

> "May I access your GitHub account?"

You authorized it once.

Now Git can push without asking for a password every time.

---

# 🐳 Docker

This was today's biggest topic.

---

## Dockerfile

You wrote:

```dockerfile
FROM python:3.14-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY . .

CMD ["python","scraper.py"]

## Why `.env` is not copied

Huge concept today.

Image contains:

```text
Python
Requirements
Code
```

NOT

```text
.env
```

Instead

```bash
docker run --env-file .env
```

temporarily injects environment variables into the container.

Nothing is permanently stored.

---

## Biggest realization

Your Python code simply does

```python
os.getenv("GEMINI_API_KEY")
```

It doesn't care whether the value comes from

* `.env`
* Docker
* GitHub Secrets
* AWS
* Azure
* Railway
* Render

The source changes.

The code doesn't.

This is exactly how professionals write portable applications.

---

# 🔥 Your Mental Model

You now have this picture in your head:

```text
Write Python Code
        │
        ▼
Git
        │
        ▼
Commit
        │
        ▼
GitHub
        │
        ▼
Docker Build
        │
        ▼
Docker Image
        │
        ▼
docker run
        │
        ▼
Container
```
Tomorrow we'll insert one more piece:

Allah Hafiz, Meerub. 🌙🤍

**creating a ci pipeline**
You do not need Ubuntu installed on your laptop.

When you push your code:

Your Laptop (Windows)
       │
       │ git push
       ▼
GitHub Repository
       │
       ▼
GitHub Actions
       │
       ▼
☁ Creates a fresh Ubuntu virtual machine
       │
       ▼
Runs your workflow
       │
       ▼
Deletes the machine after finishing

That Ubuntu computer exists only for a few minutes in GitHub's cloud.

When the workflow finishes...

🗑️ GitHub destroys it.

Next time you push?

A brand new Ubuntu machine is created again.

Imagine your teammate has:

MacBook

Another teammate has:

Windows

Another teammate has:

Ubuntu

If everyone tested on their own computers, results could differ.

Instead GitHub always says:

"Everyone's code will be tested on the same Ubuntu machine."

That's why CI is reliable.
