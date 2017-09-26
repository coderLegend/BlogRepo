---
title: git stash命令（储藏）
date: 2017-09-26 17:08:24
tags:
---
### 使用场景    
张三正在开发功能，此时张三有个紧急bug需要去修复。而正在开发的内容还没有写好，为了不丢失，就可以用上git 的储藏

### 使用说明

- 查看储藏列表  

```
git stash list // 以下是输出的内容
stash@{0}: On master: git  // stash@{0}为储藏的名字，On master: 在那个分支上 git为储藏的描述 
stash@{1}: On master: profile
stash@{2}: On master: env
```
- 储藏更改  

```
git stash save <msg> // msg 储藏描述信息
git stash -u save <msg> //-u 会把没有记录到的文件也保存下来(比如你新建了一个文件，但是还没有git add，stash也会把这个文件保存下来)
git stash -k save <msg> //-k 表示 stash之后，所有对暂存区的改变会维持不变（比如你之前add 了一个file，提交之后，git status还是能够在暂存区看到你的 add）,如果是—no-keep-index的话，stash之后的状态就是git reset —hard HEAD。
```
- 应用储藏  

```
git stash apply <stashname> 
git stash apply <stashname>  --index // --index 的选项来告诉命令重新应用被暂存的变更
```
- 撤销储藏  

```
git stash show -p stash@{0} | git apply -R // stash@{0}为储藏的名字
```
- 删除储藏  

```
git stash drop <stashname> 
```
- 清空所有的储藏

```
git stash clear
```
