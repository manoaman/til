### Git

#### How to remove .DS_Store

```
find . -name .DS_Store -print0 | xargs -0 git rm --cached --ignore-unmatch
```

https://stackoverflow.com/questions/18393498/gitignore-all-the-ds-store-files-in-every-folder-and-subfolder

https://qiita.com/ytkt/items/a2afd6be8e4f06c1ea25


#### Add to the existing repository?

```
git init
git add .
git commit -m "Add first."

git push --allow-unrelated-histories
```
https://help.github.com/en/articles/adding-an-existing-project-to-github-using-the-command-line
https://stackoverflow.com/questions/37937984/git-refusing-to-merge-unrelated-histories-on-rebase


#### How to change the URI (URL) for a remote Git repository?

```
git remote set-url origin new.git.url/here
```
https://stackoverflow.com/questions/2432764/how-to-change-the-uri-url-for-a-remote-git-repository


#### How to revert the current commit?

```
git rev-parse HEAD
git revert {hash}
git push
```

#### How to move files from one repository to another?

1. Get files ready for move

```
git clone <git repository A url>
cd <git repository A directory>
git remote rm origin
git filter-branch --subdirectory-filter <directory 1> -- --all
mkdir <directory 1>
mv * <directory 1>
git add .
git commit
```

2. Merge files into new repository

```
git clone <git repository B url>
cd <git repository B directory>
git remote add repo-A-branch <git repository A directory>
git pull repo-A-branch master --allow-unrelated-histories
git remote rm repo-A-branch
```

```
git add .
git commit
git push
```
https://gbayer.com/development/moving-files-from-one-git-repository-to-another-preserving-history/

#### How to remove a file from a repo?

```
git rm --cached somefile.txt
```


#### How to get the remote URL of the Git server?

```
git config --get remote.origin.url
```
