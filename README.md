# DevopsLab

---

# **Git & GitHub Setup | Git Commands | Token Authentication | Git Pull & Push Process**

This guide covers everything you need to know about **configuring Git & GitHub**, understanding essential **Git commands**, setting up **authentication using tokens**, and managing **Git pull & push operations**.

---

## **1. Installing & Configuring Git on Ubuntu**
Git is a **version control system** that helps developers track changes and collaborate efficiently.  

### **Step 1: Install Git**
Update system packages and install Git:
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install git -y
```

### **Step 2: Verify Git Installation**
```bash
git --version
```
If installed successfully, it will display the Git version.

### **Step 3: Configure Git (Username & Email)**
Set up your Git identity (required for commits):
```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```
Verify configuration:
```bash
git config --global --list
```

---

## **2. Connecting Git with GitHub (SSH Authentication)**
Instead of using passwords, **SSH authentication** allows secure access to GitHub.

### **Step 1: Generate an SSH Key**
```bash
ssh-keygen -t rsa -b 4096 -C "your-email@example.com"
```
Press **Enter** to save it in the default location (`~/.ssh/id_rsa`).

### **Step 2: Start SSH Agent & Add Key**
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```

### **Step 3: Copy the SSH Key**
```bash
cat ~/.ssh/id_rsa.pub
```
Copy the displayed key.

### **Step 4: Add SSH Key to GitHub**
1. **Go to GitHub** → **Settings** → **SSH and GPG keys**.
2. Click **New SSH Key** → Paste the copied key → **Save**.

### **Step 5: Test SSH Connection**
```bash
ssh -T git@github.com
```
If successful, you’ll see:
```bash
Hi your-username! You've successfully authenticated, but GitHub does not provide shell access.
```

---

## **3. GitHub Token Generation & Authentication**
Since GitHub **removed password authentication**, use **Personal Access Tokens (PATs)**.

### **Step 1: Generate a GitHub Token**
1. Go to **GitHub** → **Settings** → **Developer Settings**.
2. Click **Personal Access Tokens** → **Tokens (classic)** → **Generate new token**.
3. **Give it a name**, set an **expiration date**, and **select scopes**:
   - ✅ `repo` → Full repository access.
   - ✅ `workflow` → Access GitHub Actions.
   - ✅ `admin:repo_hook` → Manage repository hooks.
   - ✅ `delete_repo` (if needed).
4. Click **Generate Token** and **copy it**.

### **Step 2: Use Token for Git Authentication**
Replace `your-password` with the **GitHub token**:
```bash
git clone https://github.com/your-username/your-repo.git
```
When prompted for a password, **paste the token**.

### **Step 3: Save Token in Git Credentials**
```bash
git config --global credential.helper store
```
Now, Git won’t ask for credentials every time.

---

## **4. Understanding Git Commands**
Here’s a breakdown of essential Git commands:

| **Command** | **Description** |
|-------------|----------------|
| `git init` | Initialize a new Git repository. |
| `git clone <repo-url>` | Clone a repository from GitHub. |
| `git status` | Check the status of files. |
| `git add .` | Stage all changes. |
| `git commit -m "Message"` | Commit changes. |
| `git push origin <branch>` | Push local commits to GitHub. |
| `git pull origin <branch>` | Pull latest changes from GitHub. |
| `git branch <branch-name>` | Create a new branch. |
| `git checkout <branch>` | Switch branches. |
| `git merge <branch>` | Merge branches. |
| `git stash` | Save changes temporarily. |
| `git log` | Show commit history. |

---

## **5. Git Pull & Push Process in Ubuntu**
Git **pull** and **push** are used to sync changes between your **local and remote repositories**.

### **Step 1: Clone a Repository (Only Once)**
```bash
git clone git@github.com:your-username/your-repo.git
cd your-repo
```

### **Step 2: Pull the Latest Changes**
Before making new changes, update your local branch:
```bash
git pull origin main
```

### **Step 3: Make Changes & Stage Files**
Modify files, then check the status:
```bash
git status
```
Stage changes:
```bash
git add .
```
or stage a specific file:
```bash
git add filename.ext
```

### **Step 4: Commit Changes**
```bash
git commit -m "Your commit message"
```

### **Step 5: Push Changes to GitHub**
```bash
git push origin main
```

---

## **6. Merging Branches**
If working on multiple branches, merge them:

### **Step 1: Switch to Main Branch**
```bash
git checkout main
```

### **Step 2: Merge the Feature Branch**
```bash
git merge feature-branch
```

### **Step 3: Delete the Merged Branch**
```bash
git branch -d feature-branch
```

---

## **7. Common Git Issues & Solutions**
| **Issue** | **Solution** |
|-----------|-------------|
| `fatal: Authentication failed` | Use a **Personal Access Token** instead of a password. |
| `fatal: not a git repository` | Run `git init` inside the project folder. |
| `error: failed to push` | Run `git pull --rebase origin main` before pushing. |
| Merge conflicts | Manually resolve conflicts, then run `git commit`. |
| `Permission denied (publickey)` | Ensure SSH key is added to GitHub. |

---

## **8. Conclusion**
By following this guide, you can **configure Git & GitHub, authenticate using SSH or tokens, understand Git commands, and manage Git pull & push operations** effectively.
