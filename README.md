Introduction to `Git` 
==============
Myeong Lee and Kevin Lybarger
-------------

# Git and GitHub: Background and Exercise

## What you will do

Fork the class repository to your own GitHub account, clone your fork to your computer, add a short introduction file, push it back to your fork, and open a pull request so it can be merged into the class repo. Plan on 20 to 30 minutes. The step most people get stuck on is authentication, covered under Prerequisites below.

## Background

* Git is a distributed version control system for tracking changes, collaborating, and recovering prior states.
* GitHub is a hosted platform for Git repositories that adds pull requests, code review, issues, and permissions.
* Typical student workflow for contributing to a class repository: fork the upstream repo to your GitHub account, clone your fork locally, make changes on your fork, push to your fork, open a pull request to the upstream repo.

---

## Prerequisites

1. **Git installed**

   * Windows: install "Git for Windows" from git-scm.com. Use Git Bash or PowerShell.
   * macOS: Git is often preinstalled. Otherwise install via Xcode Command Line Tools or from git-scm.com.
   * Linux: install via your package manager, for example `sudo apt install git` or `sudo dnf install git`.

   Confirm the install worked:

   ```bash
   git --version
   ```

   You should see a version number, for example `git version 2.45.1`. If you see "command not found," Git is either not installed or not on your PATH.
2. **GitHub account** and the ability to sign in on the web.
3. **One-time Git identity on your machine**

   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "you@example.com"
   ```
4. **Authentication for pushes over HTTPS**

   GitHub does not accept your account password from the command line. When Git prompts you for a password, supply a personal access token instead. Set this up before class if you can.

   To create a token:

   1. On GitHub, go to **Settings**, then **Developer settings**, then **Personal access tokens**, then **Fine-grained tokens**.
   2. Select **Generate new token**. Give it a name and an expiration date.
   3. Under **Repository access**, choose **Only select repositories** and select your fork of `IT700`. You create the fork in step A, so you may need to come back here.
   4. Under **Permissions**, set **Contents** to **Read and write**.
   5. Generate the token and copy it. GitHub displays it once and never again.

   At the Git prompt, enter your GitHub username for the username and paste the token for the password. Store it in your OS credential manager when asked so you only do this once.

   If you have the GitHub CLI installed, `gh auth login` handles all of this and is faster.

---

## Exercise: Fork, edit, and contribute to the class repository

You will contribute a short introduction file to the upstream class repo and submit it via a pull request.

> Upstream repository: `https://github.com/lybarger/IT700`

### A. Fork the repository on GitHub

1. Open the upstream repo in your browser.
2. Select **Fork**. Accept defaults to create `https://github.com/<your-username>/IT700`.

### B. Clone **your fork** to your computer

1. On your fork’s page, select the green **Code** button and copy the **HTTPS** URL. Check that the URL contains your username and not `lybarger`.
2. Open a terminal:

   * Windows: Git Bash or PowerShell
   * macOS: Terminal
   * Linux: your preferred terminal
3. Move to the folder where you want the repo to live. For example:

   ```bash
   cd ~/Documents
   mkdir -p IT700-work
   cd IT700-work
   ```
4. Clone your fork and enter it:

   ```bash
   git clone https://github.com/<your-username>/IT700.git
   cd IT700
   ```
5. Verify you are inside the repo:

   ```bash
   git status
   ```

   You should see:

   ```
   On branch main
   Your branch is up to date with 'origin/main'.

   nothing to commit, working tree clean
   ```

   If you see "not a git repository," you are in the wrong folder. Run `cd IT700` and try again.

### C. Add your introduction file

Your file goes in `introductions/`. The folders named `introductions_Fall_2023/` and `introductions_Fall_2025/` hold prior cohorts. Do not add to or edit those.

1. Create a Markdown file in `introductions/` named `Lastname_Firstname.md`, following the existing example `introductions/Lybarger_Kevin.md`.

   * Use any text editor. Add your name and 1–2 sentences on research interests.
2. Stage, commit, and push to **your fork**:

   ```bash
   git add introductions/Lastname_Firstname.md
   git commit -m "Add introduction: <Your Name>"
   git push origin main
   ```

   Your fork’s default branch is `main`, so `origin main` is correct.

### D. Open a pull request to the upstream repository

1. In your fork on GitHub, click **Contribute**, then **Open pull request**. If GitHub shows a **Compare & pull request** banner, that works too.
2. Ensure the comparison is:

   * **base repository**: `lybarger/IT700`, **base**: `main`
   * **head repository**: `<your-username>/IT700`, **compare**: `main`
3. Write a brief description and click **Create pull request**.

### E. Confirm you are done

You have finished when both of these are true:

* Your pull request appears in the **Pull requests** tab of `lybarger/IT700`.
* The **Files changed** tab of your pull request lists exactly one new file under `introductions/`.

If **Files changed** is empty, your commit never reached your fork. Go back to step C2 and confirm that `git push` succeeded.

### F. Submit to Canvas

Upload the same introduction file to the corresponding Canvas assignment.

---

## Later, after your pull request is merged

Do this only once your pull request has been merged, which will be after class. Syncing brings your fork and local copy up to date with your classmates' additions.

1. Add the upstream remote once:

   ```bash
   git remote add upstream https://github.com/lybarger/IT700.git
   git remote -v
   ```

   `git remote -v` should now list both `origin`, your fork, and `upstream`, the class repo.
2. Fetch upstream updates and integrate them:

   ```bash
   git fetch upstream
   git checkout main
   git merge upstream/main
   ```
3. Push the updated main to **your fork**:

   ```bash
   git push origin main
   ```

---

## If you get stuck

The whole exercise can also be done in the GitHub web interface: fork the repo, open the `introductions/` folder, select **Add file**, then **Create new file**, commit, and open the pull request from the banner GitHub shows you. Try the command-line route first, because later work in this course assumes a working local Git setup. Do not spend the entire class period fighting an install, though. Use the web route, finish the activity, and sort out your local setup afterward.

---

## Minimal Git command reference for this exercise

```bash
# clone your fork
git clone https://github.com/<you>/IT700.git
cd IT700

# create or edit files, then:
git add <path>
git commit -m "Message"
git push origin <branch>

# set and use upstream
git remote add upstream https://github.com/lybarger/IT700.git
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```
