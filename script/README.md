#### How to extract file names and extensions?

```
filename=$(basename -- "$fullfile")
extension="${filename##*.}"
filename="${filename%.*}"
```
or
```
filename="${fullfile##*/}"
```
https://stackoverflow.com/questions/965053/extract-filename-and-extension-in-bash


#### How to exclude files on copying?

```
rsync -av --exclude='path1/to/exclude' --exclude='path2/to/exclude' source destination
```
https://askubuntu.com/questions/333640/cp-command-to-exclude-certain-files-from-being-copied
