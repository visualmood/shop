Git学习笔记
1、创建账号：
git config --global user.name "visualmood"

2、创建邮件
git config --gobal user.email "727726364@qq.com"

3、进行到操作磁盘目录
cd d:/github 

4、创建repository 本地仓库目录，并且初初化
如果目录存在，先cd d:   
然后执行  mkdir github   创建目录仓库文件夹
最后进入目录  cd githtb
git init

github文件夹中出现.git文件夹，表明仓库创建成功

5、查看状态
git status

6、添加文件到缓存区
git add readme.txt
语法1：git add file_name         指定文件名
语法2：git add file1_name file2__name file3_name...    文件名之间用空格分隔
语法3：git add .                     【添加当前目录所有文件到缓存区中 .之前有个空格】

7、提交缓冲区文件到版本库
git commit -m "注释内容"

8、版本回退
查看版本二个方法，推荐使用第二种  git log -- pretty=oneline
git log  
git log --pretty=oneline

将当前状态恢复到某个版本。
git reset --hard 版本号  可以是全部编号，也可以只复制编号前面7个字符

如果恢复到某个版本后，这时再用 git log,只能看到当前版本之前的版本，之后的版本就看不到了。
就要用到另外一个命令
git reflog    查看所有 commit和reset操作记录，从里面就可以找到版本号，

切记！此时你就明白了，为什么要写版本注释 -m'comment'.如果没有comment，你不知道状态，也就不知道何从恢复了。

9、线上仓库的创建：
	基于https，复制url:        https://github.com/visualmood/shop.git
在本地创建一个与线上同名的仓库   mkdir shop
克隆 仓库  git clone https://github.com/visualmood/shop.git

	基于 ssh
a,生成客户端公私钥文件   ssh-keygen -t rsa -C "727726364@qq.com" 
默认在C:\Users\Administrator\.ssh文件夹下生成二个文件
	id_rsa   私钥文件，这个注意保存   i
	d_rea.pub 公钥文件，存放github
b,将公钥上传到github

10、提交本地到线上仓库
git push

11、拉取线上最新版本到本地仓库
git pull

上班先pull 将线上仓库最新版本同步到本地仓库
下班再push 将本地仓库最新版本同步到线上仓库

12、查看分支
git branch
如果没有创建其它分支，则显示:*main

13、创建分支
git branch master  (这里是主分支，其它分支到时以这个作为当前分支来合并）
再创建一个分支
git branch dev_user (这是关于用户模块的分支）

14、切换分支
先查看再切换，当前分支名字前面有个星号标志
git checkout  dev_user
如果不切换分支，则后续所有git add / git commit / reset操作都是当前分支
切换分支后，当前分支做的操作，用其它分支是无法查看的。全部完成后就可以合并分支才能查看
对于一个新分支，可以合并13/14二个步骤，创建新分支并切换到该分支
git checkout -b new_branch_name

15、合并分支 先切换到主分支作为当前分支，其它被合并分支合并到当前主分支中
git checkout master  (将main 或master作为主分支）
git merge dev_user(被合并的分支名）

16、合并后，就可以删除不用的分支
删除前要退出删除的分支，否则无法删除
git branch -d dev_user(要删除的分支名）

17、冲突的产生与解决
example：
	1、A当天下班git push后，B直接在线上仓库作了更改。
	2、A第二天上班忘记 git pull，看接上代码，下班时推上线git push时产生冲突，提示信息先pull再push
	3、A此时再次git pull，然后打开产生冲突的文件，会看到git自动将二人的修改都merge在文件中，并且在修改的地方，标注了版本号。
	4、AB二人要共同确认，哪些修改保留，哪些不用，确认修改后保存文件并git add . /git commit，A再次git push到线上仓库，此时冲突完美解决

18、忽略文件 touch .gitignore
	.gitignore文件的忽略规则 ，加入规则中文件，git push将不会推到线上仓库，git pull线上向线下拉取文件也不会影响忽略的文件。
		1、#后面是注释
		2、忽略文件夹:  /directory/
		3、忽略某种类型文件: *.zip
		4、忽略某个具体文件: /dir/doc.exe
		5、不过滤某些文件，即不忽略：  !readme.txt
		 

end 退出
exit
