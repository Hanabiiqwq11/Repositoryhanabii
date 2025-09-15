# Exercise: Code Versioning and Storage with Git

## 1) Brief introduction — why store and version your code
Versioning your code keeps your progress safe and flexible. You can return to a working state when an experiment goes wrong, capture meaningful milestones as a project evolves, collaborate without overwriting each other, and move between computers without juggling zip files. In this exercise you will use Git to store and manage versions of your projects so you can work with confidence and keep a reliable record of changes.


---

## 2) Technologies for versioning code
There are several version control systems in common use. They are defined as follows:

- Git — a distributed version control system that records snapshots (commits), supports branching and merging, and works offline.
- Mercurial (hg) — a distributed version control system with a streamlined command set and similar concepts to Git.
- Subversion (SVN) — a centralized version control system where history lives on a central server and clients commit to it.

In this tutorial we will use Git. It is widely available, integrates with GitHub and Gitee, and makes local commits fast and reliable. The ideas generalize to other systems, but the commands differ.


---

## 3) Git in brief — how it works
A repository (repo) is a project folder tracked by Git. A commit is a snapshot with a short message describing what changed. A branch is a safe lane to try ideas without affecting the main line of work, and a merge brings work from one branch into another. A remote is the online copy on a service like GitHub or Gitee. In practice you edit files, stage them with add, make a commit, push to the remote, and others can pull those changes.

![Git flow diagram](images/git-flow.svg)

---

## 4) Choose your source code platform
Host your Git repository on GitHub at https://github.com. If you cannot use GitHub, use Gitee at https://gitee.com as an alternative. Follow the tutorial that matches your platform below.

---

## 5) Tutorial A — GitHub (Windows, cmd)

A) Create an account and repository
Open https://github.com and sign up if you do not already have an account. Create a new repository by selecting New, entering a name for your project, and confirming to create the repository. The repository page provides a remote URL; you will use that URL to connect your local project to GitHub in the next steps.

![GitHub: create repository](images/github-create-repo.svg)

B) Install and configure Git (one‑time on this PC)
Download Git for Windows from https://git-scm.com/download/win and install it. Open your project folder in File Explorer, click the address bar, type `cmd`, and press Enter to open Command Prompt in that folder. Set your identity so commits record who made the change:
```batch
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

C) Initialize the repo locally and push the first version
You are about to turn the current folder into a Git repository, save a first snapshot, connect it to your GitHub repository, and upload that snapshot. This establishes the link so future commits can be pushed easily.
```batch
:: Initialize Git in this folder
git init

:: Optionally add a .gitignore first (see section 7)

:: Save your current project as the first commit
git add .
git commit -m "Initial commit"

:: Connect to your GitHub repo (replace USERNAME/REPO)
git branch -M main
git remote add origin https://github.com/USERNAME/REPO.git

:: Push your versioned code to GitHub
git push -u origin main
```

D) Daily versioning routine
Each time you finish a meaningful change, create a commit and push it. Commits are your named versions; pushing stores them on GitHub.
```batch
:: Stage and commit meaningful changes
git add .
git commit -m "Describe what changed"

:: Publish your new version
git push
```

Optional — SSH (avoid password prompts after setup)
```batch
ssh-keygen -t ed25519 -C "you@example.com"
```
Copy `%USERPROFILE%\.ssh\id_ed25519.pub` to GitHub under Settings, SSH and GPG keys, then add a new SSH key. Switch the remote with: `git remote set-url origin git@github.com:USERNAME/REPO.git`.


---

## 6) Tutorial B — Gitee (Windows, cmd)

A) Create an account and repository
Open https://gitee.com/signup to create an account if needed. Use the plus menu to create a repository, give it a name, and create it. The repository page shows a remote URL; you will connect to it from your local project shortly.

![Gitee: create repository](images/gitee-create-repo.svg)

B) Install and configure Git (one‑time on this PC)
Download Git for Windows from https://git-scm.com/download/win and install it. Open your project folder, type `cmd` in the address bar, press Enter to open Command Prompt there, and set your identity so commits include your name and email:
```batch
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

C) Initialize the repo locally and push the first version
These commands initialize Git in your folder, save a first commit, connect to your Gitee repository, and upload that commit so it’s stored online.
```batch
:: Initialize
git init

git add .
git commit -m "Initial commit"

git branch -M main
git remote add origin https://gitee.com/USERNAME/REPO.git

git push -u origin main
```

D) Daily versioning routine
After meaningful changes, commit and push to save the new version online.
```batch
git add .
git commit -m "Describe what changed"
git push
```

Optional — SSH on Gitee
```batch
ssh-keygen -t ed25519 -C "you@example.com"
```
Add `%USERPROFILE%\.ssh\id_ed25519.pub` in Gitee under Settings, SSH Public Keys, then add. Switch the remote with: `git remote set-url origin git@gitee.com:USERNAME/REPO.git`.


---

## 7) Minimal .gitignore
Some files don’t need to be committed to your project’s history. Typical examples are generated build output, caches, logs, editor/OS settings, machine‑local configuration, and private files such as passwords or API keys. Use a `.gitignore` file to tell Git to skip these so your history stays clean and the repository stays small. Keep source code and the assets needed to build and run your project. Make a file named `.gitignore` in your project folder and add lines like these:
```gitignore
# Build/temp
node_modules/
build/
.dist/
.vscode/
.DS_Store
Thumbs.db
*.log
```



---

## 8) Large files (optional Git LFS)
If you must version large binaries such as .mp4, .mov, or .psd, use Git LFS:
```batch
:: One-time per machine
git lfs install

:: In your repo, track needed types
git lfs track "*.mp4"
git lfs track "*.mov"
git lfs track "*.psd"

:: Commit the LFS config
git add .gitattributes
git commit -m "chore: enable LFS for media"
```
Free plans often limit LFS storage and bandwidth.

---

## 9) What you should be able to do now
You should have a repository on GitHub or Gitee, a local repository initialized with Git, an initial commit pushed online, and the ability to make a change, commit it, and push a new version. If needed, you can also set up SSH for easier authentication and Git LFS for large files.

---

## 10) Troubleshooting (versioning)
If something goes wrong while committing or pushing, try the following quick fixes.
- Push rejected due to large files
  - Remove generated/build folders; use Git LFS for required big assets.
- Repeated login prompts
  - Complete browser sign-in when asked or switch to SSH.
- Merge conflicts
  - Open conflicted files, keep the intended lines, remove `<<<<<<<`, `=======`, `>>>>>>>`, then commit.
- Windows line endings
  - `git config --global core.autocrlf true` can help normalize line endings.

