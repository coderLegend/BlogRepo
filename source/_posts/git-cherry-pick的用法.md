---
title: git cherry-pick的用法
date: 2017-09-24 23:23:28
tags:
---
### 实际使用场景
- 张三正在开发3.0分支,此时提前发布3.0部分功能以及一些新增功能。   
解决办法： 以上个版本的提交作为新分支，把3.0上已经开发且要发布的commit的应用到新增的分支上，完善好功能，并测试好就可以去发布新版本。
- 开发项目，张三把开发的代码提交上去，导致仓库上的代码跑不起来或者打包有问题。一时半会找不到原因且测试人员在催包。   
解决办法： 把张三有问题的提交的前一次提交作为一个新分支，然后把老分支的除了张三的commit都应用到新分支上即可。

### 实践
1. 新建分支
2. 批量应用commitId

```
git log // 查看commit历史记录          
git branch <branname> <commitId> // 找到符合条件的commitId为分支 branname为分支的名字    
git cherry-pick <commitId> <commitId>  //多个commitId用空格隔开
```

- 成功的情况下,会有以下的输出 
  
```
[分支名 commitId] //应用的commit的注释    
 Date: Sun Sep 24 11:27:52 2017 +0800 // 应用的时间
 1 file changed, 1 insertion(+) // 应用的结果输出
```
- 没有成功的情况下，就是应用提交发生了冲突

```
hint: after resolving the conflicts, mark the corrected paths
hint: with 'git add <paths>' or 'git rm <paths>'
hint: and commit the result with 'git commit' //造成上面的问题的原因是，应用的某文件不在仓库里    
解决办法如下：
'git add <paths>' or 'git rm <paths>' 根据情况执行上述两个命令
git cherry-pick --continue
```

#### 解决上面的场景二
- 停止仓库相关开发人员提交代码，把有问题的分支删掉，把新分支重命名并且提交上去

```
//  把有问题的最新的commitID作为新建的分支，用来保存自己的代码
git push --delete origin branchname //把有问题的分支删掉
git branch -m branchname newBranchName //把新分支重命名
git push origin newBranchName //推送分支上去
```
- 张三解决完问题后，按照上述的方法应用到分支上。
