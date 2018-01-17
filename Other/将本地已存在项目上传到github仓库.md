#github设置ssh公钥信息
personal settings -> SSH and GPG Keys ->SSH Keys ->New SSH key
##1、Git Bash输入命令:
```
$ cat ~/.ssh/id_rsa.pub
```
##2、将生成的代码全部拷贝，填入Key处， Title处填写“id_rsa.pub”或其他任意信息，保存
##3、在Git Bash上测试:
```
$ ssh -T git@github.com
```
输出:
```
Hi XXX! You've successfully authenticated, but GitHub does not provide shell access.
```
#在GITHUB上新建一个仓库(比如helloworld)
#完成helloworld版本库的初始化--Git Bash
##1、本地建立一个Git版本库
```
$ mkdir helloworld
$ cd helloworld
$ git init
```
输出:
```
Initialized empty Git repository in C:/Users/NRY/helloworld/.git/
```
##2、在版本库中添加示例文件，如a.txt
表示把该目录下的所有文件加入到本地暂存区中
这个时候我们可以执行git status命令查看结果
```
touch a.txt
$ git add .        
```
$ git add . 或者写$ git add a.txt
##3、把本地暂存区中的文件提交到本地历史区
只有在本地历史区中的内容才能提交到github
引号里是提交的注释，建议加上
```
$ git commit -m "for test only"
```
输出
```
[master 1ff8853] for test only
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 a.txt
```
##4、为版本库添加名为origin的远程版本库
origin后面的就是github服务器中你的仓库地址(Clone with SSH  从github的repository中复制)

如果提示错误：fatal: remote origin already exists，先删除远程Git仓库，再重新添加
```
$ git remote rm origin
$ git remote add origin git@github.com:ning17/helloworld.git
```
如果执行 git remote rm origin 报错的话，可以手动修改gitconfig文件的内容
```
$ vi .git/config
```
把 [remote “origin”] 那行，整行删除
##4、把github上的文件拉下来
```
$ git pull origin master
```
如果提示错误
```
From github.com:ning17/helloworld
 * branch            master     -> FETCH_HEAD
 * [new branch]      master     -> origin/master
**fatal: refusing to merge unrelated histories**
```
则需要在$ git pull origin master 命令后面增加--allow-unrelated-histories，即
```
$ git pull origin master --allow-unrelated-histories
```
执行后可能会打开一个文本编辑器让你写提交描述。直接:x退出即可
输出:
```
From github.com:ning17/helloworld
 * branch            master     -> FETCH_HEAD
Auto-merging README.md
Merge made by the 'recursive' strategy.
 README.md | 2 ++
 1 file changed, 2 insertions(+)
```
##5、本地代码提交到github的repository
```
$ git push -u origin master
```
如果出现错误fatal: 'origin' does not appear to be a git repository  以及fatal: Could not read from remote repository ，可参考**4、为版本库添加名为origin的远程版本库**
如果出现错误
```
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'git@github.com:ning17/helloworld.git'
```
这是因为本地没有update到最新版本的项目（git上有README.md文件没下载下来)
```
$ git pull --rebase origin master
```
输出
```
From github.com:ning17/helloworld
 * branch            master     -> FETCH_HEAD
First, rewinding head to replay your work on top of it...
Applying: first commit
Applying: for test
```
在本地仓库可以查看到README.md已下载下来
如果提示Applying:add local crifanLib to github

```
$ git push origin master
```
```
git config --global user.name "ning17"
git config --global user.email "ningruyun094@163.com"
```
再查看README.md是否下载下来，是的话，重新输入git push 命令
```
$ git push origin master
```