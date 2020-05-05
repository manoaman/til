#### Adding an existing project to GitHub using the command line

1. Create a new GitHub repo

2. Initialize the local directory as a Git repository.

```
% git init
```

3. Add the files in your new local repository. This stages them for the first commit.

```
% git add .
# Adds the files in the local repository and stages them for commit. To unstage a file, use 'git reset HEAD YOUR-FILE'.
```

4. Commit the files that you've staged in your local repository.

```
% git commit -m "First commit"
# Commits the tracked changes and prepares them to be pushed to a remote repository. 
```

5. In Terminal, add the URL for the remote repository where your local repository will be pushed.

```
% git remote add origin remote repository URL
# Sets the new remote

% git remote -v
# Verifies the new remote URL
```

6. Push the changes in your local repository to GitHub.

```
% git push -u origin master
# Pushes the changes in your local repository up to the remote repository you specified as the origin.
```

https://help.github.com/en/github/importing-your-projects-to-github/adding-an-existing-project-to-github-using-the-command-line
