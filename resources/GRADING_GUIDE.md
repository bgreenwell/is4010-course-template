# 🤖 Automated Grading System Guide

## Overview

IS4010 uses a sophisticated automated grading system that provides immediate, detailed feedback on your lab submissions. This guide explains how the system works, what to expect, and how to interpret your feedback.

## 🎯 How Automated Grading Works

### **The Process**
1. **You submit** your repository URL on Canvas (or we use the one from Lab 01)
2. **Automated scripts** evaluate your GitHub repository within 24-48 hours
3. **Detailed feedback** is posted as a GitHub Issue in your repository
4. **You receive** specific guidance on improvements and celebrate successes

### **What Gets Evaluated**
- ✅ **Repository Setup**: Privacy settings, collaborator access, naming conventions
- ✅ **File Structure**: Required folders and files in correct locations
- ✅ **Code Quality**: Functionality, syntax, test case results
- ✅ **Documentation**: Markdown content, comments, required sections
- ✅ **Requirements Compliance**: Following assignment specifications

## 📊 Grading Components by Lab

### **Lab 01: Git and GitHub Fundamentals (10 points)**
| Component | Points | What's Checked |
|-----------|--------|----------------|
| Repository Exists & Accessible | 1 | Can the grading system access your repo? |
| Repository Privacy & Collaboration | 2 | Private repo with `@bgreenwell` as collaborator |
| Repository Naming | 1 | Follows naming convention (flexible) |
| Lab01 Folder | 1 | `lab01/` folder exists (case-insensitive) |
| Hello.py File | 3 | Working Python file with print statement |
| Overall Setup | 2 | Complete repository configuration |

### **Lab 02: AI-Assisted Development (10 points)**
| Component | Points | What's Checked |
|-----------|--------|----------------|
| Repository Setup | 3 | Private repo with instructor access |
| Lab02 Folder | 1 | `lab02/` folder exists (handles `labs/lab02/` too) |
| Python File Exists | 1 | `lab02.py` file in correct location |
| Python Functions | 4 | All three functions working correctly (bonus point for perfection) |
| Markdown Content | 1 | `lab02_prompts.md` with required sections |

## 🧪 Function Testing Details

### **Lab 02 Function Tests**
The system actually runs your code with real test cases:

**factorial(n)**
- Test cases: `factorial(0)` → 1, `factorial(1)` → 1, `factorial(5)` → 120
- Checks for: Correct recursive/iterative logic, edge case handling

**is_prime(number)**  
- Test cases: `is_prime(2)` → True, `is_prime(4)` → False, `is_prime(17)` → True
- Checks for: Accurate prime detection, proper boolean returns

**reverse_string(s)**
- Test cases: `reverse_string("hello")` → "olleh", `reverse_string("")` → ""
- Checks for: Correct string reversal, empty string handling

### **Common Issues Caught**
- ❌ Functions still containing `pass` statements
- ❌ Syntax errors that prevent execution  
- ❌ Logic errors (e.g., `if num % 2 == 1:` for even numbers)
- ❌ Runtime errors (undefined variables, missing imports)
- ❌ Incorrect return types or values

## 📝 Understanding Your Feedback

### **Feedback Issue Format**
When you receive feedback, it appears as a GitHub Issue with this structure:

```
🎯 Lab X Feedback - Y/10 points (Z%)

## 📊 Point Breakdown
✅ Component Name: X/X points - Success message
❌ Component Name: 0/X points - Issue description
⚠️ Component Name: X/X points - Partial credit with details

## 🎯 Areas for Improvement
[Specific guidance for components that lost points]

## 🔧 Next Steps
[Actionable steps to improve your submission]

## 💡 What's Working Well
[Recognition of successful components]
```

### **Interpreting Symbols**
- ✅ **Green checkmark**: Component completed successfully
- ❌ **Red X**: Component missing or completely incorrect
- ⚠️ **Yellow warning**: Component partially working with issues

## 🎉 Perfect Score Optimization

**No Feedback for Perfect Scores**: If you earn 10/10 points, you won't receive a feedback issue. This reduces notification noise and celebrates your success! You can always check your score in Canvas or ask questions during office hours.

## 🔧 Common Issues & Solutions

### **"Repository not accessible"**
- **Check**: Is your repository private?
- **Check**: Is `@bgreenwell` added as a collaborator?
- **Solution**: Review Lab 01 setup instructions

### **"File not found" errors**
- **Check**: File/folder naming and capitalization
- **Remember**: System handles case variations (`lab01/` vs `Lab01/`)
- **Check**: Files are in correct nested structure

### **"Function has issues (0/6 tests passed)"**
- **Debug**: Run your function manually with test inputs
- **Check**: Logic errors in conditional statements
- **Look for**: Remaining `pass` statements or incomplete implementations

### **"Missing problem sections" (Lab 02 markdown)**
- **Check**: Your markdown file has three distinct problem sections
- **Look for**: Proper heading structure (`### Problem 1`, etc.)
- **Ensure**: Code blocks are properly formatted with triple backticks

## 💬 Getting Additional Help

### **Asking Questions About Feedback**
1. **Reply to the feedback issue** with specific questions
2. **Reference the exact error** message you received
3. **Share what you've tried** to fix the issue
4. **Ask during office hours** for real-time debugging help

### **Example Good Questions**
```
Hi! I received feedback that my is_prime function has issues. I tested 
is_prime(17) and got True, which seems correct. Could you help me 
understand what other test cases might be failing?
```

```
My markdown file shows "Found 2/3 problem sections" but I think I have 
all three. Could you clarify what structure the grader is looking for?
```

## 🚀 Professional Development Benefits

This automated grading system mirrors real-world software development practices:

- **Continuous Integration**: Automated testing of your code on every submission
- **Code Review Process**: Detailed feedback similar to pull request reviews
- **Issue Tracking**: Using GitHub Issues for communication and task management
- **Quality Gates**: Ensuring code meets standards before "deployment" (grading)

## 🔄 System Improvements

The automated grading system continuously evolves based on:
- **Student feedback** about clarity and usefulness
- **Common patterns** in submissions and issues
- **New requirements** as labs become more complex

Have suggestions for improving the feedback? Share them during office hours or in the Teams channel!

---

*This guide covers the current grading system as of Fall 2025. For the most up-to-date information, always refer to individual lab instructions and the course syllabus.*