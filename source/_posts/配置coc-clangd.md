---
title: 配置coc-clangd
date: 2020-12-23 19:29:26
tags: neovim
---
# 解决找不到clangd
在配置coc.nvim下的插件coc.clangd时，安装好插件在打开cpp文件时报错提示
```
[coc.nvim] clangd was not found on your PATH. :CocCommand clangd.install will install 10.0.0.
```

# 解决方法
- nvim下输入:CocCommand clangd.install nvim会自动在后台下载clangd  
	上述方法在国内下载速度较慢，笔者等了半天都没安装好，于是选择手动安装
- 到clangd的仓库下载clangd11.0.0

# 下载clangd11.0.0
[clangd](https://github.com/clangd/clangd/releases/tag/11.0.0)
下载后运行仍然提示
```
[coc.nvim] clangd was not found on your PATH. :CocCommand clangd.install will install 10.0.0.

```
原因是coc.clangd会在环境变量文件下找clangd，因此需要ln软链接到~/.local/bin/clangd下
```
cd ~/.local/bin/clangd

touch clangd

ln -s [clangd源程序地址] ~/.local/bin/clangd

```

重新打开neovim可以发现coc.nvim正常运行！

# ln语法
ln指令的正确使用语法:
```
ln -s 1.链接目标 2.软链接
```
1.被链接的目标真实物理路径
2.对链接目标创建的符号链接

