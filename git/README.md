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
https://linuxize.com/post/how-to-change-git-remote-url/


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

#### How to undo git add?

```
git reset <filename>
```

#### How to rename a tag?

```
git tag new old
git tag -d old
git push origin :refs/tags/old
git push --tags
```

Finally, make sure that the other users remove the deleted tag. Please tell them (co-workers) to run the following command:

```
git pull --prune --tags
```

#### How to mirror a repo to another server?

```
git remote add hogehoge https://username@github.com/username/hogehoge.git
git push --mirror hogehoge
```

#### How to push a new local branch to a remote Git repository and track it too?

1. Create a new branch:
```
git checkout -b feature_branch_name
```

2. Edit, add and commit your files.

3. Push your branch to the remote repository:
```
git push -u origin feature_branch_name
```

https://www.freecodecamp.org/forum/t/push-a-new-local-branch-to-a-remote-git-repository-and-track-it-too/13222

#### How to fix "repository not found" error in Mac?

Remove git keys from keychain.

https://hacknote.jp/archives/29262/

```
$ git pull
remote: Repository not found.
fatal: repository 'https://github.com/YOUR_REPO.git/' not found
```

https://hacknote.jp/archives/29262/

#### Switching remote urls?

```
% git remote set-url origin git://new.url.here # remove and re-add

or

% git remote remove origin # remove

% git remote show origin # show remote url
```

https://stackoverflow.com/questions/16330404/how-to-remove-remote-origin-from-git-repo
https://stackoverflow.com/questions/18200248/cloning-a-repo-from-someone-elses-github-and-pushing-it-to-a-repo-on-my-github
