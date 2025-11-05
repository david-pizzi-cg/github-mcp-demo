# GitHub MCP Server Demo - DevOps Workflow Demonstration

## 🎯 Demo Scenario Overview

This project demonstrates a complete DevOps workflow using the **GitHub MCP (Model Context Protocol) Server** integration with VS Code Copilot. The scenario showcases how AI can assist in the entire software development lifecycle from issue detection to deployment.

## 📋 Demo Scenario: CSS Stylesheet Bug

### 🐛 **The Problem**
The World Clock web application has a **critical bug** - the CSS stylesheet is not loading due to a typo in the HTML file:

**File**: `index.html` (line 7)  
**Issue**: `<link rel="stylesheet" href="styls.css">` ❌  
**Should be**: `<link rel="stylesheet" href="styles.css">` ✅  

**Impact**: The entire page appears unstyled, breaking the user experience completely.

## � Workflow Diagram

```mermaid
graph TD
    A[🔍 Issue Discovery] --> B[📝 Create GitHub Issue]
    B --> C[🌿 Create Feature Branch]
    C --> D[🛠️ Local Development]
    D --> E[📤 Push & Create PR]
    E --> F[🎉 Merge & Cleanup]
    
    A1[User: Website styling broken!] --> A
    B1[Create issue with MCP tools] --> B
    C1[Branch: hotfix/css-stylesheet-typo] --> C
    D1[Fix: styls.css → styles.css] --> D
    E1[Push + Auto-link PR to issue] --> E
    F1[Merge PR + Close issue] --> F
    
    style A fill:#ff6b6b
    style B fill:#4ecdc4
    style C fill:#45b7d1
    style D fill:#96ceb4
    style E fill:#feca57
    style F fill:#ff9ff3
```

## � How to Run the Demo

### **Prerequisites**
- VS Code with GitHub Copilot
- GitHub MCP Server configured
- Live Server extension installed
- Git repository connected to GitHub

### **Quick Start**
1. **Setup**: Run the pre-demo commands above to create your demo branch
2. **Open**: Start Live Server to see the broken, unstyled page  
3. **Begin**: Use the Phase 1 prompt to start the AI-guided workflow
4. **Follow**: Use the prompts from each phase in sequence
5. **Cleanup**: Run post-demo cleanup when finished

### **Phase 0: Pre-Demo Setup** 🔧
**User Prompt:**
```
Can you create a demo branch remotely from main and switch to it.
```

### **Phase 1: Issue Discovery** 🔍
**User Prompt:**
```
Copilot, I just opened my World Clock website and it looks completely broken - all the beautiful styling is missing and it's just plain HTML. Can you investigate what's wrong with the styling?
```

**Expected AI Response:**
- Analyze HTML file for CSS link issues
- Identify the typo in `href="styls.css"`
- Explain the root cause and impact

### **Phase 2: Issue Management via GitHub MCP** 📝
**User Prompt:**
```
Now that we've found the CSS link typo, can you create a GitHub issue to track this bug? Make it a critical priority since it breaks the entire user experience. Please create the issue against the current demo branch (not main).
```

**Expected AI Actions:**
- Use `mcp_github_issue_write` to create issue
- Title: "Critical: CSS stylesheet not loading due to filename typo"
- Labels: `bug`, `critical`, `styling`
- Detailed description with file and line reference
- **Important**: Issue should reference demo branch, not main

### **Phase 3: Branch Management via GitHub MCP** 🌿
**User Prompt:**
```
Perfect! Now I need to create a branch from the current demo branch that will be properly linked to issue #6. Can you check the issue title and create a branch named using GitHub's convention: {issue-number}-{issue-title-as-slug}? This should be something like "6-critical-css-stylesheet-not-loading-due-to-typo-in-html-link" to match what GitHub would auto-generate.
```

**Expected AI Actions:**
- Use `mcp_github_issue_read` to get the exact issue title
- Convert title to GitHub's slug format (lowercase, hyphens, no special chars)
- Use `mcp_github_create_branch` from current demo branch
- **Critical**: Branch name must follow pattern: `{issue-number}-{issue-title-slug}`
- **Example**: Issue #6 "Critical: CSS stylesheet not loading due to typo in HTML link" 
  → Branch: `6-critical-css-stylesheet-not-loading-due-to-typo-in-html-link`
- **Alternative**: Suggest using GitHub UI for automatic branch creation with perfect linking
- **Best Practice**: Use GitHub UI to create branch from issue, then fetch/checkout locally

### **Phase 4: Local Development** 🛠️
**User Prompt:**
```
Great! Now let's fix the actual bug. Can you correct the CSS link typo and verify the fix works?
```

**Expected AI Actions:**
- Fix typo: `href="styls.css"` → `href="styles.css"`
- Suggest testing with Live Server
- Confirm styling is restored

### **Phase 5: Integration via GitHub MCP** 📤
**User Prompt:**
```
The fix works perfectly! Now let's commit this change and create a pull request targeting the current demo branch (not main) to get it reviewed and merged.
```

**Expected AI Actions:**
- Use `mcp_github_create_pull_request`
- **Base branch**: Current demo branch (not main!)
- **Head branch**: `6-critical-css-stylesheet-not-loading-due-to-typo-in-html-link` (or similar GitHub-generated name)
- Commit message: "Fix critical CSS stylesheet filename typo"
- PR description should include "Fixes #6" or "Closes #6" for auto-linking
- Auto-link PR to the original issue
- Add detailed PR description

### **Phase 6: Completion via GitHub MCP** 🎉
**User Prompt:**
```
Excellent! The PR looks good. Can you merge it into the demo branch and clean up the workflow?
```

**Expected AI Actions:**
- Use `mcp_github_merge_pull_request` (merges into demo branch)
- Auto-close linked issue
- Clean up feature branch
- **Result**: Demo branch now has the fix, main branch stays broken for replayability


### **Phase 7: Post-Demo Cleanup** 🔧
**User Prompt:**
```
Can you close the issue and now delete the demo branch locally and remotely?
```

#### **Benefits:**
- ✅ **Perfect Replayability**: Main always stays broken
- ✅ **Isolated Demos**: Each presentation gets clean environment  
- ✅ **Realistic Workflow**: Shows proper branch management
- ✅ **No History Pollution**: Demo artifacts are cleanly removed
- ✅ **Multiple Demos**: Can run concurrent demos with different branch names

## 📁 Project Structure

```
github-mcp-demo/
├── index.html          # Main HTML file (contains the bug)
├── styles.css          # CSS stylesheet (working correctly)
├── script.js           # JavaScript functionality
├── README.md           # This documentation
└── .vscode/
    └── mcp.json        # MCP Server configuration
```

## ⚠️ Important: GitHub MCP vs UI Branch Linking

### **GitHub UI Branch Creation (Recommended for Issue Linking)**
When you create a branch directly from a GitHub issue via the web UI:
- ✅ **Auto-generates** proper naming: `{issue-number}-{issue-title-slug}`
- ✅ **Auto-links** branch to issue in GitHub's backend
- ✅ **Example**: Issue #6 → Branch `6-critical-css-stylesheet-not-loading-due-to-typo-in-html-link`

### **GitHub MCP Branch Creation (Limited Linking)**
When using `mcp_github_create_branch`:
- ❌ **Manual naming** only - no auto-title integration
- ❌ **No automatic UI linking** (relies on naming conventions)
- ⚠️ **Workaround**: Use GitHub UI for branch creation, then fetch locally

### **Best Practice for Demo**
1. Create issue via MCP: `mcp_github_issue_write`
2. Create branch via **GitHub UI** from the issue (for proper linking)
3. Fetch and checkout locally: `git fetch origin {branch-name}`
4. Continue with MCP tools for PR creation and merging

## 🎯 Learning Objectives

This demo showcases:
- **AI-Assisted Development**: How Copilot can detect and analyze code issues
- **GitHub MCP Integration**: Seamless GitHub operations from VS Code
- **DevOps Automation**: Complete workflow from issue to deployment
- **Best Practices**: Proper branching, commit messages, and PR management
- **Collaborative Development**: Issue tracking and code reviews

## 📚 Additional Resources

- [GitHub MCP Server Documentation](https://github.com/modelcontextprotocol/servers)
- [VS Code Copilot Integration](https://code.visualstudio.com/docs/copilot)
- [DevOps Best Practices](https://docs.github.com/en/actions/guides)

---

**Ready to demonstrate the power of AI-driven DevOps workflows!** 🚀