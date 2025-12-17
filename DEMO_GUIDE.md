# CI/CD Demo Guide - Step by Step

## 📋 Overview
This guide will walk you through a complete CI/CD demo using GitHub Actions.

**Workflow:**
- Push to `feature` branch → Triggers CI
- Create Pull Request → Triggers CI
- Merge PR to `main` → Triggers CD (deployment)

---

## 🚀 Step-by-Step Demo Instructions

### **STEP 1: Initial Setup on GitHub**

1. **Create a new repository on GitHub:**
   - Go to https://github.com
   - Click "New repository"
   - Name: `cicd-demo` (or any name you prefer)
   - Make it **Public** (so GitHub Actions runs for free)
   - **DO NOT** initialize with README (we already have one)
   - Click "Create repository"

2. **Push your local code to GitHub:**
   ```bash
   # If not already initialized
   git init
   
   # Add remote (replace YOUR_USERNAME with your GitHub username)
   git remote add origin https://github.com/YOUR_USERNAME/cicd-demo.git
   
   # Add all files
   git add .
   
   # Commit
   git commit -m "Initial commit with CI/CD workflows"
   
   # Push to main branch
   git branch -M main
   git push -u origin main
   ```

---

### **STEP 2: Create Feature Branch**

1. **Create and switch to feature branch:**
   ```bash
   git checkout -b feature
   ```

2. **Make a change to the app (simulate new feature):**
   - Open `app.py`
   - Add a new function:
   ```python
   def power(a, b):
       """Raise a to the power of b"""
       return a ** b
   ```
   - Add to the main block:
   ```python
   print(f"2^3 = {power(2, 3)}")
   ```

3. **Add a test for the new feature:**
   - Open `test_app.py`
   - Add:
   ```python
   def test_power():
       assert power(2, 3) == 8
       assert power(5, 2) == 25
       assert power(10, 0) == 1
   ```

4. **Commit and push to feature branch:**
   ```bash
   git add .
   git commit -m "Add power function feature"
   git push -u origin feature
   ```

5. **🎯 OBSERVE CI IN ACTION:**
   - Go to GitHub → Your repository
   - Click "Actions" tab
   - You should see "CI - Feature Branch" workflow running
   - Click on it to see the steps executing
   - **Point out to your class:** Tests running automatically on push!

---

### **STEP 3: Create Pull Request (PR)**

1. **Create PR on GitHub:**
   - Go to your repository on GitHub
   - Click "Pull requests" tab
   - Click "New pull request"
   - Base: `main` ← Compare: `feature`
   - Click "Create pull request"
   - Title: "Add power function"
   - Description: "This PR adds a power calculation feature"
   - Click "Create pull request"

2. **🎯 OBSERVE CI ON PR:**
   - You'll see "CI - Pull Request" workflow running
   - Click "Details" to watch it
   - **Point out:** Automated checks before allowing merge
   - Wait for it to complete (green checkmark ✅)

3. **Review and approve:**
   - Scroll down and click "Merge pull request"
   - Click "Confirm merge"

---

### **STEP 4: Observe CD (Deployment)**

1. **🎯 OBSERVE CD IN ACTION:**
   - Click "Actions" tab
   - You should see "CD - Deploy to Main" workflow running
   - This was triggered automatically by the merge!
   - Click on it to watch the deployment steps

2. **Key points to show your class:**
   - ✅ Code was tested automatically
   - ✅ Only merged after CI passed
   - ✅ Deployment triggered automatically
   - ✅ Deployment artifact created
   - Click on the workflow → "Summary" → See deployment artifact

---

### **STEP 5: Demo the Complete Flow Again (Optional)**

**Make another change to demonstrate the full cycle:**

1. **Switch back to feature branch:**
   ```bash
   git checkout feature
   git pull origin main  # Get latest changes
   ```

2. **Add another function:**
   ```python
   def modulo(a, b):
       """Get remainder of a divided by b"""
       if b == 0:
           raise ValueError("Cannot modulo by zero")
       return a % b
   ```

3. **Add test:**
   ```python
   def test_modulo():
       assert modulo(10, 3) == 1
       assert modulo(15, 4) == 3
   ```

4. **Commit and push:**
   ```bash
   git add .
   git commit -m "Add modulo function"
   git push
   ```
   → **CI runs** ✅

5. **Create PR, wait for CI, merge** → **CD runs** ✅

---

## 🎓 What to Explain to Your Class

### **CI/CD Benefits:**
1. **Automated Testing:** Every push is tested automatically
2. **Early Bug Detection:** Catch issues before they reach production
3. **Code Quality:** Ensures all changes pass tests
4. **Fast Feedback:** Developers know immediately if something breaks
5. **Safe Deployments:** Only tested code reaches production

### **GitHub Actions Concepts:**
- **Workflows:** `.github/workflows/*.yml` files
- **Triggers:** `on: push`, `on: pull_request`
- **Jobs:** Tasks that run (build, test, deploy)
- **Steps:** Individual actions within a job
- **Runners:** Virtual machines that execute the jobs

---

## 📊 Demo Checklist

Use this during your presentation:

- [ ] Show the workflow files (`.github/workflows/`)
- [ ] Push to feature branch → Show CI running
- [ ] Create PR → Show CI running on PR
- [ ] Show green checkmark before merge
- [ ] Merge PR → Show CD running
- [ ] Show deployment artifacts
- [ ] Explain each workflow step
- [ ] Answer questions about triggers and jobs

---

## 🔍 Common Questions & Answers

**Q: Why do we need both CI on push and CI on PR?**
A: CI on push gives quick feedback to developers. CI on PR ensures code is tested before merging.

**Q: What happens if tests fail?**
A: The workflow shows a red X ❌ and the PR cannot be merged (if branch protection is enabled).

**Q: Can we deploy to real servers?**
A: Yes! Replace the simulation steps with real deployment commands (e.g., deploy to AWS, Heroku, etc.)

**Q: Is GitHub Actions free?**
A: Yes for public repositories. Private repos get 2000 minutes/month free.

---

## 🎯 Advanced Demo (Optional)

### Add Branch Protection Rules:

1. Go to Settings → Branches
2. Add rule for `main` branch
3. Enable "Require status checks to pass before merging"
4. Select your CI workflow
5. Now PRs **cannot** be merged if CI fails!

---

## 📝 Summary

You now have a complete CI/CD pipeline:
- ✅ Automated testing on every push
- ✅ PR validation before merge
- ✅ Automatic deployment to production
- ✅ Clear visibility of all processes

**Good luck with your demo!** 🎉
