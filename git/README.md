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
