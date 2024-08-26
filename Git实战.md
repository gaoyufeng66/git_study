# Git实战



## 第一章 快速入门

### 1.1 什么是Git

Git是一个分布式的软件版本控制软件

- 软件，类似于QQ、office、dota等安装到电脑上去才能使用的工具
- 版本控制，类似于毕业论文、写文案、视频剪辑等，需要反复修改和保留原历史数据。
- 分布式
  - 文件夹拷贝
  - 本地版本控制
  - 集中式版本控制
  - 分布式版本控制

### 1.2为什么要做版本控制

要保留之前的所有版本，以便回滚和修改

### 1.3安装Git

详见:https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git



## 第二章 “东北热”创业史

### 2.1 第一阶段：单枪匹马开始干

想要让git对一个目录进行版本控制需要以下步骤:

- 需要管理的文件夹

- 执行初始化命令

  ```
  git init
  ```

- 管理目录下的文件状态

  ```
  git status
  注：新增的文件和修改过后的文件都是红色
  ```

- 管理制定文件（红变绿）

  ```
  只管理指定文件名的文件
  git add 文件名
  将所有修改和新增的文件都管理
  git add .
  ```

- 个人信息配置：用户名、邮箱【初次配置一次即可】

  ```
  git config --global user.email "2592198859@qq.com"
  git config --global user.name "gaoyufeng"
  ```

- 生成版本

  ```
  git commit -m '版本描述信息'
  ```

- 查看版本记录

  ```
  git log
  ```

### 2.2 第二阶段：扩展新功能(短视频)

```
touch 短视频.py
git add 短视频.py
git commit -m '短视频'
```



### 2.3 第三阶段："约饭事件"

- 回滚至之前版本

```
git log
git reset --hard 版本号
```

- 回滚至之后版本

```
查看所有的版本
git reglog
git reset --hard 版本号
```

### 2.4 小总结

```
git init
git add
git commit
git log
git reflog
git reset --hard 版本号
```

![image-20240822225020681](Git实战.assets/image-20240822225020681.png)

### 2.5 第四阶段：商城&紧急修复bug

#### 2.5.1 分支

分支可以给使用者提供多个开发环境，意味着你可以把你的工作从开发主线上分离开来，以免影响开发主线。

#### 2.5.2 紧急修复bug方案

![image-20240822225347754](Git实战.assets/image-20240822225347754.png)

#### 2.5.3 命令总结

- 查看分支

  ```
  git branch
  ```

- 创建分支

  ```
  git branch 分支名称
  ```

- 切换分支

  ```
  git checkout 分支名称
  ```

- 分支合并（可能产生冲突）

  ```
  git merge 要合并的分支
  注意：切换分支在合并
  ```

- 删除分支

  ```
  git branch -d 分支名称
  ```

#### 2.5.4 工作流

![image-20240822225753698](Git实战.assets/image-20240822225753698.png)

### 2.6 第五阶段进军三里屯

有钱之后就要造呀，一个人在三里屯买了一层楼做办公室

![image-20240822225900619](Git实战.assets/image-20240822225900619.png)

#### 2.6.1 第一天上班前在家上传代码

首先，需要注册github账号，并且创还能远程仓库，然后再执行如下命令，将代码上传到github。

![image-20240822230101998](Git实战.assets/image-20240822230101998.png)

```
1. 给远程仓库起别名
git remote add origin https://github.com/gaoyufeng66/git_study.git
2. 向远程推送代码
git push -u origin 分支名称
注：-u 是指定默认的分支名称,之后可以使用git push即可自动上传到默认的分支中,前期不熟不建议使用
```

#### 2.6.2 初次在公司新电脑上下载代码

```
1. 克隆远程仓库的代码（适用于本地一点代码也没有，第一次从远程仓库拷贝代码）
git clone 远程仓库地址（内部已实现 git remote add origin 远程仓库地址）
2. 切换分支
git checkout 分支名称
```

在公司下载完代码后，继续开发

```
1. 切换到dev分支进行开发
	git checkout dev
2. 把master分支合并到dev[仅一次]
	git merge master
3. 开发修改代码
4. 提交代码
	git add .
	git commit -m 'xx'
	git push origin dev 
```

#### 2.6.3 下班回到家继续写代码

```
1. 切换到dev分支进行开发
	git checkout dev
2. 将远程仓库的代码拉下来更新本地仓库（适用于本地有代码，需要更新和继续开发的场景）
	git pull origin dev
	注：git pull 等价于 git fetch 和 git merge
3. 继续开发
4. 提交代码
	git add .
	git commit -m 'xx'
	git push origin dev
```

#### 2.6.4 回到公司继续开发

```
1. 切换到dev分支进行开发
	git checkout dev
2. 将远程仓库的代码拉下来更新本地仓库（适用于本地有代码，需要更新和继续开发的场景）
	git pull origin dev
3. 继续开发
4. 提交代码
	git add .
	git commit -m 'xx'
	git push origin dev
```

。。。。一直这样循环

#### 2.6.5 开发完毕，准备上线

```
1. 将dev分支合并到master分支，进行上线
	git checkout master
	git merge dev
	git push origin master
2. 把dev分支也推到远程代码仓库
	git checkout dev
	git merge master
	git push origin dev
```

#### 2.6.6 在公司约妹子忘记提交代码

```
1. 在公司拉代码
	git pull origin dev
	发现没有在公司写的代码
2. 在公司开发其他功能
	git add .
	git commit -m 'xx'
3. 由于和妹子吃饭忘记push
```

#### 2.6.7 到家继续写代码

```
1.  到家拉取代码（发现没有更新，发现在公司写的代码忘记提交）
	git pull origin dev
2.	开发其他功能
3.	把dev分支推送到远程
	git add .
    git commit -m 'xx'
    git push origin dev
```

#### 2.6.8 到公司继续写代码

```
1. 在公司拉取代码，把在家写的代码拉取到本地（有合并，可能会产生冲突）
	当同一个代码文件，同一行写入的内容不一样时会产生冲突
	git pull origin dev
2. 手工解决冲突
3. 继续开发其他功能
4. 把dev分支推到远程
	git add .
	git commit -m 'xx'
	git push commit dev
```

#### 2.6.9 git pull

```
直接将远程代码仓库的dev拉取并合并到本地dev中
git pull origin dev
等价于
先将远程仓库的代码拉取到本地的版本库中
git fetch origin dev
再讲版本库中拉到的最新的代码合并到工作区中
git merge origin/dev
```

![image-20240823000547245](Git实战.assets/image-20240823000547245.png)

#### 2.6.9 rebase的作用？

##### 2.6.9.1 rebase场景一：将多个版本记录合并为一个版本记录

rebase可以保证提交记录简洁，不分叉 ，可以将多个版本合并为一个版本

==尽量不要将已经移交到远程代码仓库的版本（已push的版本）进行合并，不然会因代码版本记录不一致而产生问题==

```
touch 1.py
git add .
git commit -m 'v1'

touch 2.py
git add .
git commit -m 'v2'

touch 3.py
git add .
git commit -m 'v3'

touch 4.py
git add .
git commit -m 'v4'

git log

可以用以下两个方法将将版本合并
git rebase -i 版本号
git rebase -i HEAD~3
注意：修改后要用wq命令保存，需要合并版本将前面的pick修改为s，表示将V3和V4版本合并为V2版本
```

将pick修改为s

```
（ i 是插入,dd 是删除一行 :wq是保存  :q!是强制退出）
```

![image-20240825153904334](Git实战.assets/image-20240825153904334.png)

给合并后的版本起一个名字

![image-20240825154133862](Git实战.assets/image-20240825154133862.png)

最终版本效果如下图所示

![image-20240825154357948](Git实战.assets/image-20240825154357948.png)

##### 2.6.9.2 rebase场景二：将dev分支合并到master分支并只有一条分支

将dev分支合并到主分支，只有一条分支

```
git log版本记录分支图形化
git log --graph
git log版本记录分支图形化简洁版（只有版本号和版本名称）
git log --graph --pretty=format:"%h %s"

只想有一个分支，将dev分支删掉并合并到master分支中
git checkout dev
git rebase master 
git checkout master
git merge dev
```

##### 2.6.9.3 rebase场景三：git pull 可以替换为 git fetch 和 git rebase

```
正常拉取数据：
git pull origin dev
替换为（也可以将dev分支合并到master分支并只有一条分支）：
git fetch origin dev
git rebase origin/dev
```

注意：git rebase 产生冲突

场景：在master分支和在dev分支修改了同一个文件，产生冲突

![image-20240825200634061](Git实战.assets/image-20240825200634061.png)

解决方案: 

```
解决冲突文件
git add .
git rebase --continue
然后确认版本名称(会自动弹出)
git checkout master
git merge dev
```

#### 2.6.10 Araxis merge工具的使用（快速解决冲突）

首先找到配置文件路径  ==C:\Users\gaoyufeng\.gitconfig==

自定义notepad++快捷键（Ctrl + Shift + C 复制当前文件路径 Ctrl + Shift + D 打开当前文件所在位置）

将配置文件修改为如下内容：其中 araxis merge的路径替换为系统真实路径

```
[i18n]
	commitencoding = utf-8
	logoutputencoding = utf-8
[core]
	quotepath = false
[user]
	name = gaoyufeng
	email = 2592198859@qq.com
[http]
	sslVerify = false
[diff]
    external = \"D:\\Araxis\\Araxis Merge\\araxisgitdiff.exe\"
[mergetool "araxis"]
    cmd = \"D:\\Araxis\\Araxis Merge\\araxisgitmerge.exe\" \"$BASE\" \"$LOCAL\" \"$REMOTE\" \"$MERGED\"
    trustExitCode = true
[mergetool]
keepBackup = false

[merge] 
tool = araxis
stat = true
```

当使用merge或者pull产生冲突时，可以用 git mergetool 冲突文件名 来快速处理冲突

注意：也可以使用beyond compare 来处理

#### 总结

-  添加远程代码仓库链接

  ```
  git remote add origin 地址
  ```

-  推送代码

  ```
  git push origin dev
  ```

- 下载代码

  ```
  git clone 地址
  ```

- 拉取代码

  ```
  git pull origin dev
  等价于
  git fetch origin dev
  git merge origin/dev
  ```

- 保持代码提交整洁（变基）

  ```
  git rebase 分支
  ```

- 记录的图形展示

  ```
  git log --graph --pretty=format:"%h %s"
  ```

### 2.7 第六阶段 多人协同开发工作流

#### 2.7.1 创建项目&邀请成员

协同开发时，需要所有成员都可以对同一个项目进行操作，需要邀请成员并赋予权限，否则无法开发。

github支持两种创建项目的方式（供多人协同开发）

​	1.合作者，将用户添加到仓库合作者中之后，该用户就可以向当前仓库提交代码。collaborators(合作者)

![image-20240826152802293](Git实战.assets/image-20240826152802293.png)

​	2.组织，将成员邀请进入组织，组织下可以创建多个仓库，组织成员可以向组织下仓库提交代码。

![image-20240826153103890](Git实战.assets/image-20240826153103890.png)

![image-20240826153144584](Git实战.assets/image-20240826153144584.png)

##### 扩展：Tag标签管理

为了能清晰的管理版本，在公司不会直接使用commit来做版本，会基于Tag来实现：V1.0、V1.2、V2.0 版本。

在commit后面打了一个tag标签

```
创建本地创建Tag信息
git tag -a v1.0 -m '版本介绍'
删除Tag
git tag -d v1.0
将本地tag信息推到远程仓库
git push origin --tags
更新本地tag版本信息
git pull origin --tags

切换tag
git checkout v1.0
指定tag下载代码
git clone -b v0.1 地址
```

2.7.2 公司其他同事开发

- 先注册github或gitlab账号
- 邀请公司同事进入组织（默认对组织中的项目有读权限）

![image-20240826162833067](Git实战.assets/image-20240826162833067.png)

- 邀请同事成为项目的合作者

![image-20240826162910752](Git实战.assets/image-20240826162910752.png)

- 同事下载项目到自己的电脑上开发

  ```
  从远程代码仓库下载代码
  git clone https://github.com/oldboy-org/dbhot.git
  切换目录
  cd dbhot
  切换到dev分支
  git checkout dev
  切换并创建ddz分支
  git checkout -b ddz
  开发，写代码...
  
  git add .
  git commit -m '斗地主功能开发完成'
  git push origin ddz
  ```

#### 2.7.3 code review

1.配置，代码review之后才能合并到dev分支

![image-20240826164551488](Git实战.assets/image-20240826164551488.png)![image-20240826164622768](Git实战.assets/image-20240826164622768.png)

2.同事提交code review 申请

![image-20240826164653560](Git实战.assets/image-20240826164653560.png)

![image-20240826170430908](Git实战.assets/image-20240826170430908.png)

3.组长做code review

![image-20240826170501279](Git实战.assets/image-20240826170501279.png)

![image-20240826170514282](Git实战.assets/image-20240826170514282.png)

#### 2.7.4 测试上线（预发布）

由专业团队或团队leader执行以下步骤：

 1.基于dev分值创建release分值

```
git checkout dev
git checkout -b release
```

2.测试

3.合并到master

```
使用pull request
本地将release合并到master分值
```

4.在master分支上打tag标签

```
git tag -a v2 -m '第二版 斗地主功能'
git push origin --tags
```

5.运维人员下载代码做上线

```
git clone -b v2 地址
```

2.9 第七阶段：给开源软件贡献代码

1.fork源代码 将比尔呢源代码拷贝到我自己的远程仓库。

2.在自己仓库进行代码修改

3.给源代码的作者提交 修复bug的申请（pull request）

## 第三章 其他

3.1 配置

- 项目配置文件：项目/.git/config

  ```
  git config --local user.name '高玉峰'
  git config --local user.email '2592198859@qq.com'
  ```

- 全局配置文件:~/.gitconfig

  ```
  git config --gloabl user.name = 'gaoyufeng'
  git config --global user.email = '2592198859@qq.com'
  ```

- 系统配置文件：/etc/.gitconfig

  ```
  git config --system user.name 'gaoyueng'
  git config --system user.email '2592198859@qq.com'
  ```

应用场景:

```
git config --local user.name '高玉峰'
git config --local user.email '2592198859@qq.com'
git config --local merge.tool bc3
git config --local mergetool.path '/usr/local/bin/bcomp'
git config --local mergetool.keepBackup false
git remote add origin 地址 (--local) (默认添加在本地配置文件中)
```

### 3.2 免密码登录

- URL中体现

  ```
  原来的地址: https://github.com/gaoyufeng66/dbhot.git
  修改的地址: https://用户名:密码@github.com/gaoyufeng66/dbhot.git
  
  git remote add origin https
  git push origin master
  ```

- SSH实现

  ```
  1.生成公钥和私钥（默认放在 ~/.ssh 目录下,id_rsa.pub 公钥/id_rsa私钥）
  ssh-keygen
  2.拷贝公钥的内容，并设置到github中
  3.在git本地中配置ssh地址
  git remote add origin git@github.com:gaoyufeng/dbhot.git
  
  4.以后使用
  git push origin master
  ```

- git自动管理凭证

### 3.3 git忽略文件

让git不再管理当前目录下的某些文件

```
*.h
!a.h
files/
*.py[c|a|d]
```

更多参考：https://github.com/github/gitignore

### 3.4 github任务管理相关

- issues，文档及任务管理
- wiki，项目文档





