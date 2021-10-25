---
layout:     post
title:      VS Code path setup
date:       2021-10-17
author:     Aniket
summary:    Setting up vscode extension path in windows and much more.
categories: Editors
thumbnail:  vscode
tags:
 - windows
 - editor
---

If you are like me and just hate seeing your C drive fill up or just like to have a clean C drive then this post is for you.
By deafult almost all of VS Code are stored in `C:\Users\UserName\.vscode\extensions`(for the time being will be talking about windows only) and you dont want that, right?

# Portable Version
Just use portable version. Go to VS Code [download page][1] and download `.zip` file. In portable version everything from user profile to extensions will be stored in a single folder with other VS Code files. Just cut-paste this folder wherever you wish to manage storage.

# Use \--extensions-dir \<dir-path>
According to VS Code[ extension management documentation][2], we can use `code --extensions-dir <dir-path>` command to specify directory path from where VS Code will try to load and later save extensions. Writing this same command again and again is the final solution? Of course not.

## Use shortcut target
For this we need to create a shortcut for VS Code. We can also use pre-existing shortcut . Right click on shortcut and add `--extensions-dir=<dir-path` at the end of the target field.
![Example of shortcut target][3]

## Change code.cmd
Whenever we run `code` command, insted of executing `code.exe` binary it lauches a script. This script file is located inside bin directory, which itself is inside directory where VS Code itself is installed i.e. `...\Microsoft VS Code\bin\code.cmd`. If you dont know where this folder is then you can simply use `where code` command to find the location. \
Now we just need edit code.cmd file.
```sh
@echo on
setlocal
set VSCODE_DEV=
set ELECTRON_RUN_AS_NODE=1

"%~dp0..\Code.exe"  "%~dp0..\resources\app\out\cli.js" --extensions-dir Path\To\Desired\Directory\%*
endlocal
```
And on that note we can add additonal flags(a full list of flags available [here][4]) to change directory for 

[1]: https://code.visualstudio.com/download
[2]: https://code.visualstudio.com/docs/editor/extension-marketplace#_command-line-extension-management
[3]: https://i.postimg.cc/t483z5FD/example-shortcut-target.png
[4]: https://code.visualstudio.com/docs/editor/command-line#_advanced-cli-options