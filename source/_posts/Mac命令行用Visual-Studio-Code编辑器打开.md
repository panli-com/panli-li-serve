title: Mac命令行用Visual Studio Code编辑器打开
date: 2015-11-09 15:12:22
tags:
  - 前端开发编辑器
  - vscode
  - 开发工具
categories:
  - 开发工具
---

## Visual Studio Code 不卡了

前些日子一直在用 Atom  编辑器 ，很喜欢代码的面向，可用了些时间后 感觉越来越卡。
于是上手 Visual Studio Code，听说不卡！ O(∩_∩)O哈哈~

## Setting up Visual Studio Code

Getting up and running with VS Code is quick and easy. Follow the platform specific guides below as well as the list of handy tools.

### Mac OS X

1. [Download Visual Studio Code](http://go.microsoft.com/fwlink/?LinkID=534106) for Mac OS X.
2. Double-click on VSCode-osx.zip to expand the contents.
3. Drag Visual Studio Code.app to the Applications folder, making it available in the Launchpad.
4. Add VS Code to your Dock by right-clicking on the icon and choosing Options, Keep in Dock.


>Tip: If you want to run VS Code from the terminal, append the following to your ~/.bash_profile file (~/.zshrc in case you use zsh).

```
code () { VSCODE_CWD="$PWD" open -n -b "com.microsoft.VSCode" --args $* ;}
```

Now, you can simply type code . in any folder to start editing files in that folder.

参考 https://code.visualstudio.com/Docs/editor/setup