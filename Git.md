`git init`
- This creates a git repository in the folder

`git remote add origin https://github.com/your-username/your-repo-name.git
`
- This line links your **local** Git repository to your **GitHub** repository.

`git add .`
- This stages **all** files in your vault for tracking.

`git commit -m "Initial commit - adding Obsidian notes"
- This **saves** your changes with a message describing them.

`git branch -M main`
`git push -u origin main`
- This uploads your notes to GitHub and sets `main` as the default branch.


After Creating a repository if we need to update
`git add .
`git commit -m "Updated notes"
`git push origin main`

`