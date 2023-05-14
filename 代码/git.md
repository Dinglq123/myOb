## 项目初始化
```git
git init
```
## 查看状态
```bush
git status
```
## 提交修改
把文件添加到暂存区
```bush
// 单个文件
git add fileName

// 所有文件
git add .
```
提交修改
```bush
git commit -m "change description"
```
## 版本回退
查看版本log
```
// 查看基于当前版本'HEAD'的更改记录
git log

// 查看历史的
git reflog
```
回退版本
当前版本是`HEAD`，前一个版本是`HEAD^`，前两个版本时`HEAD^^`，前一百个版本是`HEAD~100`。
```bush
// 回退上一个版本
git reset hard HEAD^
// 回退指定版本
git reset hard number
```
## 删除文件
使用`git rm fileName`可以从版本库删除文件，需要再使用`git commit`来更新版本库。
```bush
// 删除文件
git rm fileName
// 更新版本库
git commit -m "delete fileName"
```
## 撤销修改
`git checkout`:用版本库里的版本替换工作区的版本。
使用`git checkout --fileName`可以使`fileName`文件在工作区的修改全部撤销。分为两种情况：
- `fileName`自从修改后还没放入到暂存区：撤销修改回到版本库的状态
- `fileName`修改后被放入了暂存区：撤销修改**恢复到暂存区的状态**
```bush
git checkout --fileName
```
使用`git reset HEAD fileName`可以**把暂存区的修改撤销，重新放回工作区**，同时需要再使用`git checkout --fileName`来丢弃工作区的修改。
```bush
git rest HEAD fileName
```

