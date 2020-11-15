# Git

#### 1.本地库初始化

命令：git init

#### 2. 设置签名

命令： 

- 项目级别/仓库级别： 仅在当前本地库范围内有效
  - git config *user.name tom_pro*
  - git config *user.email giasfjsd@qq.com*
  - 保存位置：./.git/config 文件
- 系统用户级别： 登录当前操作系统的用户范围
  - git config --global *user.name 用户名*
  - git config --global *user.email 邮箱*

#### 3.基本操作

**1. 状态查看操作**

- git status			//查看工作区，暂存区状态

**2. 添加操作**

- git add [file name]			//将工作区的“新建/修改”添加到暂存区

**3. 提交操作**

- git commit -m "commit message" [file name]			// 将暂存区的内容提交到本地库

**4. 查看历史记录操作**

- git log									//最完整的日志显示
  - 多屏显示控制方式：
    - 空格向下翻页
    - b 向上翻页
    - q 退出

- git log --pretty=online        //一行显示
-  git log --online                 //一行显示
- git reflog                            //一行显示
  - 显示内容：HEAD@{移动当前版本的步数}

**5. 前进后退**

- 基于索引值的操作[推荐]
  - git reset --hard [局部索引值]
  - git reset --hard a6ace91
- 使用 ^ 符号 只能后退 （一个符号一个版本）
- 使用~符号 只能后退 ~3（数字为后退版本个数）

**6. reset命令的三个参数对比**

- --soft 参数
  - 仅仅在本地库移动指针
- --mixed参数
  - 在本地库移动HEAD指针
  - 重置暂存区
- --hard参数
  - 仅仅在本地库移动指针
  - 重置暂存区
  - 重置工作区

**7 删除文件并找回**

- 前提： 删除前， 文件存在时的状态提交到了本地库
- 操作 ：git reset --hard [版本]
  - 删除操作已经提交到本地库：指针位置指向历史记录
  - 删除操作尚未提交到本地库：指针位置使用 HEAD

**8 比较文件差异**

- git diff [文件名]
  - 将工作区中的文件和暂存区比较
- git diff [本地库中历史版本]
  - 将工作区中的文件和本地库历史文件比较
- 不带文件名比较多个文件

#### 4 分支操作

- 创建分支
  - git branch [分支名]
- 查看分支
  - git branch -v
- 切换分支
  - git checkout [分支名]
- 合并分支
  - 第一步：切换到接受修改的分支上
    - git checkout [分支名]
  - 第二步：执行merge命令
    - git merge [分支名]
- 解决冲突
  - 第一步：编辑文件，删除特殊符号
  - 第二步：把文件修改到满意的程度， 保存退出
  - 第三步：git add [文件名]
  - 第四步：git commit -m "日志信息"          （这里不可以带文件名）

#### 5 连接远程库

- git remote -v 查看当前所有远程地址别名
- git remote add \[别名][远程地址]

#### 6 推送

- git push \[别名][分支名]

#### 7 克隆

- git clone [地址]
  - 完整把远程库下载到本地
  - 创建远程地址别名
  - 初始化本地库

**windows凭据管理器可以删除账号**

#### 8 拉取

- pull = fetch + merge

- git fetch \[远程库地址别名][远程分支名]
- git merge \[远程库地址别名/远程分支名]
- git pull \[远程库地址别名][远程分支名]

#### 9 解决冲突

- 如果不是基于远程库的最新版本所做的修改，不能推送，必须先拉取
- 拉取下来如果进入冲突状态，则按照“分支冲突解决操作”解决

#### 10 跨团队协作

- fork               (网页操作）
- pull requests     （网页操作）