# Beginner Git and GitHub Tutorial

This document is separate from the main project notebook. It explains how to save the completed project with Git and publish it on GitHub using Windows.

## 1. What Git and GitHub mean

**Git** is a program installed on your computer. It records changes to files so you can return to an earlier version if needed.

**GitHub** is a website that stores Git repositories online. It makes the project available as an online portfolio and gives you a link to submit.

The difference is simple: Git works locally on your computer, while GitHub hosts a copy of the Git project online.

## 2. Install Git on Windows

Open the official [Git website](https://git-scm.com/download/win) in a browser and download Git for Windows. Run the installer and keep the recommended default options.

After installation, open **Git Bash** or **Command Prompt** and type:

```text
git --version
```

This command asks Git to display its installed version. You should see something similar to `git version 2.x.x`. If Windows says that `git` is not recognized, close and reopen the terminal. If the problem continues, reinstall Git and make sure the option to add Git to the PATH is enabled.

## 3. Create or check your GitHub account

Open [github.com](https://github.com/) and create an account if you do not already have one. Verify your email address and sign in. Do not put your GitHub password, personal access token, or API keys inside the project files.

## 4. Organize the project folder

Create one folder for the project. For example:

```text
github-machine-learning-analysis
```

Place the master notebook and the supporting data folders inside it. The recommended structure is:

```text
github-machine-learning-analysis/
├── github_repository_analysis_project.ipynb
├── data/
│   ├── raw/
│   │   └── github_repositories_raw.json
│   └── clean/
│       └── github_projects.csv
├── figures/
│   ├── top_10_repositories_by_stars.png
│   ├── repositories_by_language.png
│   └── stars_and_forks_scatter.png
└── .gitignore
```

The helper scripts used while developing can be included if your teacher wants to see them. The main file to submit is `github_repository_analysis_project.ipynb`.

## 5. Create a `.gitignore` file

A `.gitignore` file tells Git which files should not be uploaded or tracked. Create a plain-text file named exactly `.gitignore` in the project folder and add:

```text
# Python temporary files
__pycache__/
*.py[cod]

# Jupyter temporary files
.ipynb_checkpoints/

# Secrets and local settings
.env
.env.*
*.key
*.pem
secrets.json

# Operating-system files
.DS_Store
Thumbs.db

# Temporary outputs and logs
*.log
```

Never upload API keys, passwords, access tokens, private certificates, or environment files containing credentials. The current project uses a public GitHub endpoint and does not need a secret API key. If an API key is required in a future project, store it in a local `.env` file and read it through an environment-variable library. Do not write the actual key in the notebook.

## 6. Open a terminal in the project folder

In File Explorer, open the project folder. Click the address bar, type `cmd`, and press Enter. A Command Prompt window will open in that folder.

You can check the folder contents with:

```text
dir
```

You should see the notebook, `data` folder, `figures` folder, and `.gitignore` file.

## 7. Initialize Git

Type this command in the terminal opened inside the project folder:

```text
git init
```

This creates a hidden `.git` folder. Git uses that folder to store the project history. You should see a message saying that an empty Git repository was initialized.

Check the repository status:

```text
git status
```

This shows which files are untracked or changed. A new project will usually show several untracked files.

## 8. Set your Git name and email

Use the name and email that you want recorded in your commits:

```text
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

Replace the example values with your own information. These commands usually produce no output. You can check the settings with:

```text
git config --global user.name
git config --global user.email
```

## 9. Add the project files

Stage all files that are not excluded by `.gitignore`:

```text
git add .
```

The period means “add files from this project folder.” The command normally produces no output. Check what is staged:

```text
git status
```

Files shown in green under “Changes to be committed” are ready for the first commit. If a secret appears in the list, stop and remove it before continuing.

## 10. Create the first commit

Create a saved version of the project:

```text
git commit -m "Complete GitHub repository analysis project"
```

The `-m` option adds a short description of the commit. You should see a summary of the files and lines added.

Check the commit history:

```text
git log --oneline
```

You should see the new commit with a short identifier and the message.

## 11. Create a repository on GitHub

On GitHub, click the plus sign in the top-right corner and choose **New repository**. Use a simple name such as:

```text
github-machine-learning-analysis
```

Add a short description. Choose **Public** if your teacher requires a public submission. When creating the repository, do not add another README, `.gitignore`, or license if those files already exist locally. This avoids an unnecessary merge conflict.

After creating the repository, GitHub displays the repository URL. Copy the HTTPS URL. It will look similar to:

```text
https://github.com/YOUR-USERNAME/github-machine-learning-analysis.git
```

## 12. Connect the local project to GitHub

In the terminal inside the local project folder, type:

```text
git remote add origin https://github.com/YOUR-USERNAME/github-machine-learning-analysis.git
```

Replace `YOUR-USERNAME` and the repository name with your real values. This command tells the local project where its online GitHub repository is located.

Check the connection:

```text
git remote -v
```

You should see the GitHub URL listed for `origin`.

If Git says that `origin` already exists, check the current URL with `git remote -v`. If it is wrong, replace it with:

```text
git remote set-url origin https://github.com/YOUR-USERNAME/github-machine-learning-analysis.git
```

## 13. Push the project to GitHub

Rename the current local branch to `main`:

```text
git branch -M main
```

Push the commit to GitHub:

```text
git push -u origin main
```

The first push may ask you to sign in. GitHub no longer accepts a normal account password for command-line Git authentication. Use the sign-in method requested by GitHub, such as browser authentication or a personal access token. Never write the token in the notebook or commit it to the project.

After a successful push, open the repository page in your browser and refresh it. You should see the notebook, CSV, raw JSON, figures, and any included documentation.

## 14. Check the uploaded project

Open the notebook on GitHub and check that its sections and outputs are visible. Open each figure to confirm that the charts are readable. Check that no `.env` file, password, API key, or token was uploaded.

Copy the repository URL into the final notebook’s submission-evidence section if your teacher wants the link inside the project file. Take the required screenshots of the GitHub repository page and successful Git commands, then add the screenshot filenames to that section. The rubric specifically requires the repository link and screenshots.

## 15. Make future changes

When you edit the notebook or add a file, use this sequence from the project folder:

```text
git status
git add .
git commit -m "Update analysis and documentation"
git push
```

`git status` checks what changed. `git add .` stages the changes. `git commit` saves them as a new local version. `git push` uploads the new commit to GitHub.

## 16. Common problems

If Git says `not a git repository`, the terminal is not inside the project folder. Use File Explorer to open the correct folder and open a new terminal there, or use `cd` with the folder path.

If Git says `nothing to commit`, there are no new changes since the last commit. Check the files and run `git status`.

If Git says that the remote repository was not found, check the URL with `git remote -v`. Make sure the repository exists and that the username and repository name are spelled correctly.

If GitHub rejects a file because it is too large, remove unnecessary files and keep only the notebook, required data, figures, and documentation. Do not upload temporary logs, caches, or large unrelated files.

If a secret was accidentally committed, do not only delete it from the current folder. The secret may still exist in Git history. Revoke or replace the secret immediately, remove it from the project, and ask your teacher or an experienced user for help cleaning the Git history.

## Short command summary

```text
git --version
git init
git status
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
git add .
git commit -m "Complete GitHub repository analysis project"
git remote add origin https://github.com/YOUR-USERNAME/REPOSITORY.git
git branch -M main
git push -u origin main
```
