# Git

---

### 设置名字和邮件地址

因为git是分布式版本控制系统，所以每个机器都必须自报家门

```bash
git config --global user.name "Jyn"
git config --global user.email "jyn725@outlook.com"
```



## 创建版本库

---

### 1.创建目录

```bash
mkdir learngit
cd learngit
pwd
```



### 2.通过`git init`命令把当前目录变为git可以管理的仓库

```bash
git init
```

如果没有看见`.git`目录，那是因为这个目录是隐藏的，使用`ls -ah`就可以看见



### 3.通过`git add`命令告诉git，把文件添加到仓库

```bash
git add readme.md  // git add file_name
git add .	// 添加所有的文件
```



### 4.通过`git commit`告诉git，把文件提交到仓库

```bash
git commit -m 'add a file readme.md'
```

为什么git提交文件需要`add`, `commit`两步呢？因为一次`commit`可以提交很多文件，所以可以多次add文件，然后一次commit提交。如

```bash
git add file1.md
git add file2.md file3.md
git commit -m 'add 3 file3'
```



## 版本回退

---

### `git status`可以让我们掌握仓库的当前状态，上面命令告诉我们，有哪些更改，新增，更新，删除...

```bash
git status
```



### `git diff`可以查看difference，显示的格式正是Unix通用的diff格式

```bash
git diff
```



### `git log`命令显示的是最近到最远的提交日志

```bash
git log	// 查看提交历史

git log --pretty=online // 显示进行了优化
```

首先git要知道当前版本是哪个版本，在git中，用`HEAD`表示当前版本，上一个版本是`HEAD^`，上上个版本是`HEAD^^`，当然往上100个版本写100个`^^^^`比较容易数不过来，所以写成`HEAD-100`

我们来回退到上一版本 

```bash
git reset --hard HEAD^
```

回退到制定的某个版本

```bash
git reset --hard 109421e
```

### 在git中总是有后悔药可以吃的，git提供了一个`git reflog`用来记录你的每一次命令

```bash
git reflog	// 查看命令历史
```



## 工作区和暂缓区

---

`git add`命令实际上就是把工作区的文件提交到暂缓区，然后执行`git commit`命令就可以一次把暂缓区文件提交到分支

<u>**暂缓区是git非常重要的概念，弄明白了暂缓区，就明白git的很多操作到底干了什么**</u>



## 撤销修改

---

`git checkout -- file`可以丢弃工作区的修改

```bash
git checkout -- readme.md
```

命令`git checkout -- readme.md`意思是，把readme.txt在工作区的修改全部撤销，这里有两种情况：

- 一种是`readme.md`自修改后还没放到暂缓区，现在撤销修改就回到和版本库一模一样的的状态
- 一种是`readme.md`已经添加到暂缓区，又做了修改，现在，撤销修改就回到添加到暂缓区的状态

<u>**总之，就是回到文件最近一次`git commit`或`git add`的状态**</u>

`git reset`既可以回退版本，也可以把暂缓区的修改回退到工作区，当我们用`HEAD`时，表示最新版本

```bash
git reset HEAD readme.md
```



**场景一：当改乱了工作区某个内容，想直接丢弃工作区的修改时，用命令`git checkout --file`**

**场景二：不但改乱了工作区的内容，还添加到了暂缓区，想丢弃修改，分两步**

1. `git reset HEAD <file>`，就回到了场景一
2. 场景一



## 删除文件

---

本地已经删除，再从版本库删除并提交

```bash
git rm test.txt

git commot -m 'remove test.txt'
```

删除错了，因为版本库里面还有呢，轻松恢复文件到最新版本

```bash
git reset -- test.txt
```

命令`git rm`用于删除一个文件，如果一个文件已经提交到版本库，不用担心误删，但是要小心，只能回复文件到最新版本，会丢失最后一次修改的内容。



## 添加远程库

---

