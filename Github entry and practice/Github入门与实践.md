# 1. 安装 GitHub

安装网址: http://msysgit.github.io/

## 1.1 初始设置

- 设置名字和邮箱地址

```markdown
$ git config --global user.name "Firstname Lastname"
$ git config --global user.email "your_email@example.com"
```

这个命令 会在“~/.gitconfig”中输出以下形式的文件

	[user]
		name = Firstname Lastname
		email = your_email@example.com

- 提高命令输出可读性

```
$ git config --global color.ui auto
```

  会在“~/.gitconfig”中增加下面这一行

```
[user]
	ui = auto	
```

## 1.2 设置 SSH

- 设置SSH Key

```
$ ssh-keygen -t rsa -C "your_email@example.com"
```

会在 /c/Users/用户名/.ssh下建立两个文件 `id_rsa`  私有密钥 和 `id_rsa.pub` 公开密钥

- 查看公开密钥

```
$ cat ~/.ssh/id_rsa.pub
```

全部复制，在 GitHub 的 Setting 中



# 2. github的小知识点

快捷键  `shift + /`

Download ZIP 相比 clone的劣势：

1. 无法查看日志

2. 无法对仓库进行重修

3. 适合只是想用仓库中的文件

仓库页面 `按t` ,输入要查找的目录和部分文件的名字

明确指向仓库文件某一行 `URL + "#L10"`  或者 某几行 `"#L10-L15"`

## 2.1  查看差别

样例网址：https://github.com/rails/rails/

- 查看分支差别
	
	https://github.com/rails/rails/compare/4-0-stable...3-2-stable
	
- 查看与几天前的差别

  https://github.com/rails/rails/compare/master{7.day.ago}...master

- 查看指定日期之间的差别

  https://github.com/rails/rails/compare/master{2013-01-01}...master
  
  

## 2.2 Issue

- Tasklist语法

  复选列表样式：

- [x] 123

- 在相关issue中显示已经提交的`Issue`

  在 `Issue` 中提及其他 `Issue` 使用 `Issue` 对应的编号如：“#24”

- 引用评论

  选中相关文字部分 `按R`  

- 表情

  `：+字母`  自动补全表情

issue 与 pull request编号通用

## 2.3 Pull Request

在 File Change 中 查看文件更改内容以及前后差别

- 忽略空格差别在URL 末尾添加 `?w=1`
- 在代码左侧点击`+`号可以对相应代码添加评论



## 2.4 Wiki

简介: 在网络上开放且可供多人协同创作的超文本系统

​      GitHub 每一个项目都有一个独立完整的 Wiki 页面，我们可以用它来实现项目信息管理，为项目提供更加完善的文档。我们可以把 Wiki 作为项目文档的一个重要组成部分，将冗长、具体的文档整理成 Wiki，将精简的、概述性的内容，放到项目中或是 README.md 里。

## 2.5 Setting

- feature

	可以更改显示或者关闭 Wiki和Issue等相关设置

- Github Pages

	有一个名为GitHub Page的库，用户可以利用该仓库中的资料创建Web页

- Deploy Keys

用于部署的公开密钥，用户可以使用私有密钥通过ssh协议clone仓库

# 3 . 通过实际操作学习 git

## 3.1 基本操作

- git init ------- 初始化仓库

```
$ mkdir git-tutorial
$ cd git git-tutorial
$ git init
```

- git status ------ 查看仓库状态

```
$ touch README.md
$ git status 
```

- git add ------ 向暂存区添加文件

```
$ git add README.md
$ git status
```

- git commit ------ 保存仓的历史记录

```
$ git commit -m "First commit"
```

省去  `-m ` 进行详细提交 

提交规范

1. 第一行： 文字简述提交更改内容
2. 第二行：空行
3. 第三行： 记述更改原因和详细内容

- git log ------ 查看提交日志

```
$ git log
$ git log --pretty=short // 只显示提交的第一行
$ git log README.md // 只显示指定目录、文件日志
$ git log -p  // 显示文件改动
$ git log -p README.md
```

- git diff ------查看更改前后差别			

```
$ git diff
$ git diff HEAD  // 查看工作树和最新提交的差别
```

# 4.4 推送到远程仓库





# 4. 尝试 Pull Resquest

在网络上也简称PR。

## 4.1 发送Pull Request 的前期准备

登录准备的网址 : https://ituring.github.io/first-pr/

![1](C:\Users\Administrator\Desktop\读书笔记\Github entry and practice\图片\1.png)

- Fork
	先 Fork 创建到自己的仓库
- clone

```
$ git clone git@github.com:wzyys1/first-pr.git
$ cd first-pr
```

- branch

  1.  先创建特性分支再修改代码
  2.  确认分支

```
$ git branch -a
```

​		  3. 创建特性分支

​				创建一个名为 `work` 的特性分支

```
$ git checkout -b work gh-pages
```

​				再次确认切换到了work分支下

```
$ git branch -a 
```

​				查看文件列表，可以看到网站中显示的 index.html文件

```
$ ls
```

​			4. 添加代码

```
省略
<p>您如果有对本书的读后感，或者只是想单纯测试一下，都可以发送Pull Request。</p>
↓追加的行
<p class="impression"> 这本书读着很有趣。 (@名字) </p>
```

​			5. 提交修改

```
$ git diff
$ git add index.html
$ git commit -m "Add my impression"
```

​			6. 远程创建分支(创建本地work分支相应的远程分支)

```
$ git push origin work
$ git branch -a 
```

## 4.2 发送 Pull Request

登录网页，切换到对应分支，发送。

## 4.3 总结

   1.fork 到自己的库 

2. clone下来 
3.  建个新分支 
4. 修改 
5. 创建远程分支 
6.  页面找到 Pull Request  
7. 发送

## 4.4 仓库的维护



![2](C:\Users\Administrator\Desktop\读书笔记\Github entry and practice\图片\2.png)

​		我们需要将原仓库设置为远程仓库，从该仓库获取（fetch）数据与本地仓库进行合并（merge），让本地的仓库的源代码保持最新状态。

​		这里以下面网址为例:https://github.com/octocat/Spoon-Knife

1. 先Fork到自己的仓库

2. clone下来

```
$ git clone git@github.com:octocat/Spoon-Knife.git
$ cd Spoon-Knife
```

3. 给原仓库起名字 ，添加新的远程仓库

```
$ git remote add upsteam git@github.com:octocat/Spoon-Knife.git
```

4. 获取新数据

```
$ git fech upsteam
From github.com:octocat/Spoon-Knife
 * [new branch]      change-the-title -> upsteam/change-the-title
 * [new branch]      main             -> upsteam/main
 * [new branch]      test-branch      -> upsteam/test-branch

$ git merge upsteam/master
Already up to date.
```

# 5. 接收 Pull Request

## 5.1 采纳的方法

​	直接 `merge Pull Request` 就行

​	但是一般在采纳之前， 会将接收到的 `Pull Request` 拿到本地开发环境中检查，确认能否正常进行以及代码是否安全。

## 5.2 采纳前的准备

- 代码审查

  可以在 `File Changed` 的某行进行评论， 发送方和接收方都会收到 Notifications

- 在本地开发环境中反映 Pull Request 的内容![3](C:\Users\Administrator\Desktop\读书笔记\Github entry and practice\图片\3.png)

  1. 将接收方的本地仓库更新到最新状态

     clone 到本地，如果已经存在，pull 更新到最新状态
```
$ git clone git@github.com:ituring/first-pr.git
$ cd first-pr
```

​			2. 获取发送方仓库

```
$ git remote add PR发送者 git@github.com:PR发送者/first-pr.git
$ git fetch PR发送者
```

​			3. 创建用于检查的分支

![4](C:\Users\Administrator\Desktop\读书笔记\Github入门与精通\图片\4.png)

```
$ git checkout -b pr1
```

​			4. 合并

```
$ git merge PR发送者/work
```

​			5. 删除分支
```
$ git branch -D pr1
```

## 5.3 采纳 Pull Request

- 方法一 --- 浏览器

  打开浏览器找出相应的 Pull Request 界面，点击 `Mege pull request`

  ![5](C:\Users\Administrator\Desktop\读书笔记\Github entry and practice\图片\5.png)

- 方法二 --- 命令行操作

  只要通过命令行 进行合并操作，再 `push` 至 GIthub, `Pull Request` 中就会 反映出 `Pull Request` 被采纳后的状态

![6](C:\Users\Administrator\Desktop\读书笔记\Github entry and practice\图片\6.png)

- 合并到主干分支

```
$ git checkout  gh-pages
$ git merge PR发送者/work
```

- push 修改内容

保险起见，先看差别再push

```
$ git diff 
$ git push
```

用这种方法处理后， 仓库的 `Pull Request` 会自动从  `Open `  状态变为 `Close` 状态。