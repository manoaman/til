### Python

#### Conda

Update conda

```
conda update -n base conda
```

Create virtual env

```
conda create -n <my env> <install module>
#  conda create --name snowflakes biopython
```

Check virtual env

```
conda info -e
```

Remove virtual env

```
conda remove -n <my env> --all
# conda remove -n snowflakes --all
```

https://qiita.com/showsuzu/items/e2fddf22f725f4d2ab8c

#### How to sort dict?

```
mydict = {
    "carl": 40,
    "alan": 2,
    "bob": 1,
    "danny": 3,
}

for key in sorted(mydict.keys()):
    print("%s: %s" % (key, mydict[key]))
```
https://www.saltycrane.com/blog/2007/09/how-to-sort-python-dictionary-by-keys/

---

#### PIP

List, instal, and uninstall

```
% pip list
% pip install <module>
% pip uninstall <module>
```


