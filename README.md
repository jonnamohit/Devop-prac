# 🚀 DevOps Practice - Hello World CI/CD Pipeline

## Project Overview

This project demonstrates a complete **CI/CD (Continuous Integration/Continuous Deployment)** pipeline using GitHub Actions. It includes an interactive frontend dashboard that explains how the pipeline works.

## 📁 Project Structure

```
Devop-prac/
├── .github/
│   └── workflows/
│       └── hello-world-build.yml      # CI/CD Pipeline Configuration
├── frontend/
│   ├── index.html                     # Interactive Dashboard
│   ├── style.css                      # Styling
│   ├── script.js                      # Interactive Features
│   └── README.md                      # Frontend Documentation
├── PIPELINE_GUIDE.md                  # Complete Pipeline Guide
├── hello.py                           # Sample Python Script
├── README.md                          # This File
└── .git/                              # Git Configuration
```

## 🎯 What This Project Does

1. **CI/CD Pipeline:** Automatically builds and tests code when you push changes
2. **Frontend Dashboard:** Visual explanation of the pipeline
3. **Documentation:** Complete guide on how to check and understand the pipeline

## 🔍 Quick Start

### **VIEW THE PIPELINE - On GitHub**
1. Go to: https://github.com/jonnamohit/Devop-prac/actions
2. Click on latest workflow run
3. Expand "build" job to see all steps
4. Click each step to view logs

### **VIEW THE PIPELINE - Local Frontend**
1. Open `frontend/index.html` in your browser
2. See visual pipeline flow
3. Follow the step-by-step guide
4. Links to GitHub Actions

### **TRIGGER A NEW PIPELINE RUN**

```bash
# Make a change
echo "test" >> file.txt

# Commit and push
git add .
git commit -m "Testing pipeline"
git push origin main
```

## 📊 Pipeline Flow

```
Code Push → Checkout → Build → Test → Deploy
```

## 📚 Documentation Files

- **PIPELINE_GUIDE.md** - Complete guide on how pipeline works
- **frontend/README.md** - Frontend dashboard guide
- **frontend/index.html** - Interactive dashboard (open in browser)

## 💻 How to Check Pipeline Status

1. Visit GitHub Actions: https://github.com/jonnamohit/Devop-prac/actions
2. Click latest "Hello World Build Pipeline" run
3. Expand "build" job to see all steps
4. Click each step to view console output

## 🎓 When Does Pipeline Run?

- When you push to `main` branch
- When you push to `develop` branch  
- When you create a pull request

## 🚀 Common Commands

```bash
git status                              # Check changes
git add .                               # Stage all changes
git commit -m "Your message"            # Commit changes
git push origin main                    # Push & trigger pipeline
git log --oneline -5                    # View recent commits
```

## 🔗 Quick Links

| Link | Purpose |
|------|---------|
| [GitHub Actions](https://github.com/jonnamohit/Devop-prac/actions) | Check pipeline status |
| [Repository](https://github.com/jonnamohit/Devop-prac) | GitHub repository |
| [Workflow File](.github/workflows/hello-world-build.yml) | Pipeline configuration |
| [Pipeline Guide](PIPELINE_GUIDE.md) | Detailed documentation |

## 📖 Learning Path

1. Read this README
2. Open `frontend/index.html` in browser
3. Visit GitHub Actions page
4. Push some code to trigger pipeline
5. Read `PIPELINE_GUIDE.md` for details

## 🎯 Next Steps

1. View the Dashboard: Open `frontend/index.html`
2. Check GitHub Actions: Visit the Actions tab
3. Push Some Code: Trigger the pipeline
4. Read Full Guide: Check `PIPELINE_GUIDE.md`

---

**Repository:** jonnamohit/Devop-prac | **Branch:** main | **Purpose:** DevOps Practice
