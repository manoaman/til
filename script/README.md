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
