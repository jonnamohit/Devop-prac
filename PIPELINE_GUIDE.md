# 📚 Complete Guide: How to Check and Understand the CI/CD Pipeline

## What is a CI/CD Pipeline?

**CI (Continuous Integration):** Automatically builds and tests code when you push changes.  
**CD (Continuous Deployment):** Automatically deploys the tested code to production.

---

## 🎯 Our Pipeline: Step-by-Step Explanation

### **The Workflow File Location:**
- **File:** `.github/workflows/hello-world-build.yml`
- **Purpose:** Defines what happens when you push code

### **When Does It Trigger?**
- When you `git push` to `main` branch
- When you `git push` to `develop` branch  
- When a Pull Request is created

---

## 📊 Pipeline Flow Diagram

```
┌─────────────────┐
│   Code Push     │
│  (git push)     │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   GitHub Event  │
│  (Detected)     │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Create Runner  │
│ (Ubuntu Linux)  │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Checkout Code  │ ← Step 1: Clone repository
│  (git clone)    │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Print HelloWorld│ ← Step 2: Build step
│  (echo "hello")  │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   Run Tests     │ ← Step 3: Test step
│ (python script) │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Build Complete │ ← Step 4: Success!
│  (Deployment)   │
└─────────────────┘
```

---

## ✅ Pipeline Steps Explained

### **Step 1: Checkout Code**
```yaml
- name: Checkout code
  uses: actions/checkout@v3
```
- **What it does:** GitHub clones your repository code into the runner
- **Why:** The runner needs access to your code to build it
- **Output:** All your files are now available in the virtual machine

### **Step 2: Print Hello World (Build)**
```yaml
- name: Print Hello World
  run: |
    echo "Hello world"
```
- **What it does:** Executes the echo command that prints "Hello World"
- **Why:** Demonstrates the build process
- **Output:** "Hello world" message in the logs

### **Step 3: Test Step**
```yaml
- name: Test Step
  run: |
    echo "Running tests..."
    python hello.py
```
- **What it does:** Runs tests (in this case, executes the Python script)
- **Why:** Validates that code works correctly
- **Output:** Test results in the logs

### **Step 4: Build Complete**
```yaml
- name: Build Step
  run: |
    echo "Build completed successfully!"
```
- **What it does:** Final step confirming successful completion
- **Why:** Signals end of pipeline
- **Output:** Success message

---

## 🔍 How to Check Pipeline Status - Step by Step

### **Method 1: GitHub Web Interface (Easiest)**

1. **Go to GitHub Actions:**
   - Open: https://github.com/jonnamohit/Devop-prac/actions
   - Or click "Actions" tab in your GitHub repo

2. **View Workflow Runs:**
   - You'll see a list of workflow runs
   - Latest run is at the top
   - Green ✓ = Success
   - Red ✗ = Failed
   - Yellow ⏳ = Running

3. **Click on a Workflow Run:**
   - Select "Hello World Build Pipeline" from the list
   - See overall status and timestamp

4. **Expand the "build" Job:**
   - Click arrow to expand all steps
   - See all 4 steps with their status

5. **View Step Details:**
   - Click on each step name to see console output
   - Click "Print Hello World" to see the echo output
   - Click "Test Step" to see test results

6. **Check Full Logs:**
   - Scroll down to see complete console output
   - Search for keywords with Ctrl+F

### **Method 2: Using Git Commands (CLI)**

```bash
# View recent commits and their status
git log --oneline -10

# See which branch you're on
git branch

# View git history with details
git log --graph --oneline --all

# Check local workflow file
cat .github/workflows/hello-world-build.yml
```

### **Method 3: GitHub CLI (if installed)**

```bash
# List recent workflow runs
gh run list --repo jonnamohit/Devop-prac

# View specific run details
gh run view <run-id> --repo jonnamohit/Devop-prac

# Watch workflow in real-time
gh run watch --repo jonnamohit/Devop-prac
```

---

## 🚀 How to Trigger a New Pipeline Run

### **Trigger Method 1: Push Code Change**
```bash
# Make a change to any file
echo "changes" >> file.txt

# Stage changes
git add .

# Commit with message
git commit -m "Testing pipeline"

# Push to main branch (triggers pipeline)
git push origin main
```

### **Trigger Method 2: Push Empty Commit**
```bash
# Push without code changes
git commit --allow-empty -m "Trigger pipeline"
git push origin main
```

### **Trigger Method 3: Create Pull Request**
```bash
# Create new branch
git checkout -b feature/test

# Make changes
echo "test" >> newfile.txt

# Push branch
git push origin feature/test

# Create PR on GitHub (triggers pipeline)
# Go to GitHub and click "Compare & pull request"
```

---

## 📈 Understanding Pipeline Status Indicators

| Status | Meaning | Action |
|--------|---------|--------|
| 🟢 Success | All steps passed | Pipeline completed successfully |
| 🔴 Failed | One or more steps failed | Check logs to see which step failed |
| ⏳ In Progress | Pipeline is running | Wait for completion |
| ⭕ Queued | Waiting to run | Pipeline will start soon |
| ⚪ Skipped | Step was not executed | Check conditions/rules |

---

## 🔧 Understanding the Workflow Configuration

### **Workflow Triggers** (in `hello-world-build.yml`)
```yaml
on:
  push:
    branches: [ main, develop ]    # Runs on push to main or develop
  pull_request:
    branches: [ main, develop ]    # Runs on PR to main or develop
```

### **Runner Configuration**
```yaml
runs-on: ubuntu-latest   # Virtual machine: Ubuntu Linux (latest version)
```
- **Options:** `ubuntu-latest`, `windows-latest`, `macos-latest`
- **What it means:** GitHub provides free virtual machines to run tasks

### **Jobs and Steps**
```yaml
jobs:
  build:                    # Job name
    runs-on: ubuntu-latest  # Where it runs
    steps:                  # List of actions to perform
      - name: Step name
        run: command        # Shell command to execute
```

---

## 💡 Tips for Debugging Pipeline Issues

### **If Pipeline Fails:**

1. **Check the Error Message:**
   - Go to failed step in GitHub Actions
   - Read the error message at the bottom
   - Common errors: syntax issues, missing files, permission denied

2. **Expand All Steps:**
   - Click each step to see full output
   - Look for RED text (error messages)

3. **Check Exit Codes:**
   - 0 = Success
   - Non-zero (1, 2, etc.) = Failure

4. **Common Issues & Solutions:**

| Problem | Solution |
|---------|----------|
| `command not found` | Install the required tool/package |
| Permission denied | Check file permissions |
| File not found | Check file path is correct |
| Syntax error | Review YAML indentation |

### **Test Locally:**
```bash
# Test commands locally before pipeline
bash .github/workflows/hello-world-build.yml  # Won't work, but you get the idea
# Or manually run individual commands
```

---

## 🎓 What to Look for in Logs

### **Successful Output:**
```
✓ Checkout code completed
✓ Print Hello World completed
Hello world
✓ Test Step completed
✓ Build Step completed
Workflow completed successfully!
```

### **Failed Output:**
```
✗ Run command failed
Error: command not found
Exit code: 1
Workflow failed!
```

---

## 📱 Frontend Display

Visit the frontend at: `frontend/index.html`
- Shows pipeline status visually
- Displays pipeline flow diagram
- Links to GitHub Actions
- Shows how to trigger pipeline
- Provides all commands needed

---

## 🔗 Quick Links

- **GitHub Actions (Check Status):** https://github.com/jonnamohit/Devop-prac/actions
- **Repository:** https://github.com/jonnamohit/Devop-prac
- **Workflow File:** `.github/workflows/hello-world-build.yml`
- **Troubleshooting:** https://docs.github.com/en/actions

---

## 📝 Summary

1. **Push Code** → 2. **GitHub Detects** → 3. **Spins up VM** → 4. **Runs Steps** → 5. **Reports Results**

Every push to `main` triggers the pipeline automatically. Check status on GitHub Actions page. Expand each step to see what happened. Logs show all command output.

---

Good luck! 🚀
