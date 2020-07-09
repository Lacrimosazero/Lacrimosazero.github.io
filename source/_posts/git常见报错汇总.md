---
title: git常见报错汇总
date: 2020-07-09 09:57:08
tags:
- git
categories:
- 工具
---
### 1.如果输入`git remote add origin git@github.com:git账号名/git项目名.git`提示出错信息：`fatal:remote origin already exists`
解决办法如下：
1. 先输入`git remote rm origin`
2. 再输入`git remote add origin git@github.com:git账号名/git项目名.git `就不会报错了
3. 如果输入`git remote rm origin` 还是报错的话，`error: Could not remove config section 'remote.origin'.` 我们需要修改`gitconfig`文件的内容

### 2.`git clone`时显示`Filename too long`的解决办法
在`git bash`中，运行下列命令：` git config --global core.longpaths true` 就可以解决该问题。
`--global`是该参数的使用范围，如果只想对本版本库设置该参数，只要在上述命令中去掉--global即可。

### 3.`Git`操作失败并提示`Another git process seems to be running in this......`
Git操作的过程中突然显示`Another git process semms to be running in this repository, e.g. an editor opened by ‘git commit’. Please make sure all processes are terminated then try again. If it still fails, a git process remove the file manually to continue… `
翻译过来就是git被另外一个程序占用，重启机器也不能够解决。
原因在于Git在使用过程中遭遇了奔溃，部分被上锁资源没有被释放导致的。
解决方案：进入项目文件夹下的 `.git`文件中（显示隐藏文件夹或`rm .git/index.lock`）删除`index.lock`文件即可。

### 4.`warning: LF will be replaced by CRLF in` 解决办法
原因是存在符号转义问题
`windows`中的换行符为 `CRLF`， 而在`linux`下的换行符为`LF`，所以在执行`add .` 时出现提示，解决办法：`git config --global core.autocrlf false`

### 5.`git` 推送出现 `"fatal: The remote end hung up unexpectedly"` 解决方案
在使用git更新或提交项目时候出现` "fatal: The remote end hung up unexpectedly "` 原因是推送的文件太大。
解决方案：`git  config  http.postBuffer  524288000`

### 6.`Git error： hint: Updates were rejected because the remote contains work that you do hint: not have locally. This is usually caused b`

![](https://lacrimosa-bed.oss-cn-hangzhou.aliyuncs.com/img/6.jpg)

解决办法：
`$ git pull origin master`
`$ git push origin master`

### 7.`git`中`Please enter a commit message to explain why this merge is necessary.`

![](https://lacrimosa-bed.oss-cn-hangzhou.aliyuncs.com/img/7.png)

请输入提交消息来解释为什么这种合并是必要的
git 在pull或者合并分支的时候有时会遇到这个界面。可以不管(直接下面3,4步)，如果要输入解释的话就需要:
1.按键盘字母` i `进入`insert`模式
2.修改最上面那行黄色合并信息,可以不修改
3.按键盘左上角`Esc`
4.输入`:wq`,注意是冒号+wq,按回车键即可
