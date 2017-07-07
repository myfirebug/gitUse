# gitUse
git使用教程
# 1.1 Git 是什么？
```
Git是一种版本控制器
```
# 1.2 安装
```
Git在linux,max,win下都可以安装
本文是以win7系统为环境编写的

Window环境：
到http://git-for-windows.github.io/ 下载软件并安装

到开始菜单下找“git bash”
```
# 1.3	自报家门
```
git config --global user.name #你是谁
git config --global user.emial #怎么联系你
```
# 1.4 代码管理
## 1.4.1创建版本库
```
cd e:/
mkdir domo
git init
注意：
1、不要把仓库建在中文目录下，可能出现问题
2、.git 是个隐藏目录，不要乱动
```
## 1.4.2添加文件
```
在：e:/demo目标下，用自己喜欢的编辑器
开发你的你的程序，比如：index.txt

Echo ‘helo word’

查看仓库状态
Git status
Git add .  或者 git add index.txt  (添加到暂存区)
Git commit -m ‘add index.txt’ （提交到版本库）
```
## 1.4.3修改文件
```
如果修改了文件，也不要忘记提交到版本库（这个过程和添加文件是一样的）
git add index.txt
git commit -m ‘edit index.txt’
```
## 1.4.4删除文件
```
用rm命令删除文件，并直接commit提交到版本库
例如：先创建一个add.txt

Git add .
Git commit -m ‘add add.txt’

//开始删除

Git rm add.txt
Git commit -m ‘remove add.txt’
```
# 1.5远程仓库
## 1.5.1注册git在线仓库的帐号
```
http://github.com
```
## 1.5.2创建项目
```
在github注册后，新建项目，我们先建一个测试项目，叫text
```
## 1.5.3把代码捡到远程仓库
```
1、为本地库添加远程库
git remote add origin https://github.com/myfirebug/text.git;
意思：添加一个远程库，代号是origin,地址是https://github.com/myfirebug/text.git 
2、push推代码
git origin master
意思是，把本地的版本（默认是master），捡到代号为origin的远程库去。
这个过程会让你输入用户名/密码，即你注册时的帐户密码

或者git push https://github.com/myfirebug/text.git master
意思是把本地的master推送到远程仓库去
```
## 1.5.4团队合作
```
首先进入github 进入相应的仓库点击settings->collaborators 在右边的文本框中输入合作的名称（这里里以resourceMap举例）点击add collaborator按钮会给对方的发一封邮件等待对方确认就可以了

//模拟resourceMap用户

cd f:
git clone https://github.com/myfirebug/text.git;
```
# 2代码管理
## 2.1工作区和版本库
```
如果你想清晰的学习git你必须要了解3三个重要的区域
1、工作区，即开发者的工作目标
2、暂存区，修改已被记录，但尚未录入版本库的区域
3、版本库，存储变化日志及版本信息
```
## 2.2改动日志
```
每个文件/目录发生的版本变化，我们都可以追述
命令：git log
常用格式：
git log 查看项目的日志
git log <file> 查看某个文件的日志
git log . 查看本目录的日志

git log --pretty=oneline 让日志单行显示
``` 
# 3分支管理
```
在开发中，遇到这样的情况怎么样？
网站已有支付宝在线支付功能，要添加微信支付
修改了2个文件index.txt,config.txt
刚做到一半，突然有个紧急bug,支付宝支付后不能修改订单状态
你需要立即马上修改这个bug,需要修改的文件是a.txt,config.txt;
问题：config.txt已经被修改过，而且尚未完成
直接在此基础上改，肯定出问题
把comfig.txt倒回去，那我之前做的工作就白费了
此时你肯定会想在做微信支付时，能否把仓库复制一份，在此副本上修改，不影响原仓库的内容，修改完完毕后，再把副本上的修改合并过去
好的，这时你已经有了分支的思想
前面见过的master，即是代码的主干分支
事实上，在实际的开发中，往往不不会直接修改和提交到master分支上
而是创建一个dev分支，在dev分支上，修改测试，没问题，在把dev分支合并到master上
如果有了分支，刚才的难题就好解决了
 a.txt,config.txt
Master 							master111 					master1112222
index.txt,config.txt
 
在做微信支付时，我们创建一个wxchart分支
把wxchart分支commit,此时，master分支内容不会变，因为分支不同
 
当遇到紧急bug，创建一个bug分支
修改bug后，把bug分支合并到master分支上
 
再次从容切换到wxchart分支上，接着开发微信支付功能，开发完成后，把wxchart分支合并到master分支上
``` 
## 3.1查看分支
```
命令：git branch
```
## 3.2创建分支
```
命令：git branch wxchart   //创建dev分支
```
## 3.3切换分支
```
Git checkout wxchart 
```
## 3.4合并分支
```
当我们在dev上 开发某功能并测试通过后，可以把dev的内容合并到master分支上
首页要切换到master分支
Git checkout master
Git merge dev
``` 
## 3.5删除分支
```
Git branch -d dev
```
## 3.6快速创建和切换分支
```
Git checkout -b dev
```
# 4远程仓库
## 查看远程仓库：
```
Git remote
查看远程仓库地址：
Git remote -v
 
## 删除远程库别名
Git remote remove <远程库名>
##添加远程库
Git remote add <远程库名> <远程库地址>
```
# 5公钥登录
```
我们push酝仓库到远程时，总要输入用户名，密码很不方便
配置公钥，可以避免频繁输入用户名密码的麻烦
 
 
1、配置公钥ssh格式的远程仓库地址
例：
Git remote add origin git@github.com:myfirebug/text.git
 
2、创建ssh key
Ssh-keygen -t rsa -c ‘myfirebug.com’把邮件地址换成你自己的邮件地址，回车即可，可以在用户主目录里找到.ssh目录，内有id_rsa放id_rsa.pub两个文件，id_rsa是私钥，id_rsa.pub是公钥,这两把钥匙是成对的，可以让分别持有私钥和公钥的双方相互认识
3、把公钥放在服务器
用词本打开id_rsa.pub复件公钥内容
登录github.com
 
Settings->SSH add GPG keys 
 

版本回退:
Git reset --hard HEAD^ 回退一个版本
Git reset --hard 版本号

Git reflog  查看版本号
```
