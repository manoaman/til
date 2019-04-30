# Visual Studio Code

### XML format
```
Command + Shift + P

Type: Format code
```

### How to open a file without a preview mode?

1. Open the Command Palette using the shortcut Ctrl+Shift+P.
2. Type Preferences: Open User Settings, this will open the Settings editor. Search for workbench.editor.enablePreview, and uncheck the checkbox. (changes are autosaved and indicated with a blue left border)

https://stackoverflow.com/questions/43705543/how-to-open-file-in-new-tab-in-visual-studio-code/43707807

### How to setup vertical rulers?

To configure it, go to File > Preferences > Settings and add this to to your user or workspace settings:

```
"editor.rulers": [80]
```

