# 1/Git基本配置
1. 查看git版本：`git --version`
2. 查看git的配置文件：`cat ~/.gitconfig`，编辑：`vim ~/.gitconfig`
3. 查看用户名：`git config --global user.name`
`git config --global user.email`
4. 配置SSH：
（1） 查看是否创建id_rsa.pub文件：`cd ～/.ssh`
（2）如果未创建则创建id_rsa.pub文件：`$ ssh-keygen -t rsa -C "youremail@example.com"`
（3）查看SSH私钥：`cat ~/.ssh/id_rsa.pub`
（4）如果以前配置过SSH，可以用此命令检查连接是否正确：`$ ssh -T git@github.com`

# 2/完成Git和Github的绑定

1. 在Github上，一般都是通过SSH来授权的，而且大多数Git服务器也会选择使用SSH公钥来进行授权，所以要想向Github提交代码，首先需要在Github上添加SSH key配置。

2. 对于Linux和Mac系统，默认安装了SSH，Windows系统在安装了Git Bash后，也自带了SSH，可以通过在Git Bash中输入命令查看是否安装SSH：ssh

3. 然后输入命令：ssh-keygen -t rsa，表示我们指定RSA算法生成密钥，然后敲三次回车，中途不需要输入密码，之后会生成id_rsa（密钥）和id_rsa.pub（公钥）文件，所在目录为：

   Linux和Mac：~/.ssh中；Windows：C:\Documents and Settings\username\\.ssh

4. 之后则需要把公钥id_rsa.pub的内容添加到Github上，这样我们本地的密钥和Github上的公钥才可以匹配，才能提交代码。

   > 点击Github中头像——Settings——SSH and GPG keys——New SSH key

   > 在命令行输入：cat ~/.ssh/id_rsa.pub查看并复制公钥，粘贴到上述key中即可，Titles内容填自己能识别的名称即可，对应的邮箱也会收到添加key的邮件。

5. 通过命令验证是否绑定成功：ssh -T git@github.com

# 3/提交代码到Github

1. 两个关键命令：pull和push；pull表示如果我们远程仓库代码有了更新，为了保持本地与远程的同步，需要拉取远程代码到本地，命令：git pull origin master；

   push表示如果我们本地代码更新，为了保持本地与远程同步，需要把本地代码推送到远程仓库，命令：git push origin master

   一般如果我们fork了别人的项目，并对其做了修改，我们就需要向原始代码中提交一个pull request，然后等待作者验证；一般进行push之前，都需要先进行pull操作。

2. 提交代码有两种情况，一种是本地没有Git仓库，我们可以直接从远程仓库clone到本地。通过clone命令创建的仓库，本身就是一个Git仓库，不需要我们再进行init初始化操作，而且自动关联远程仓库。只需要我们在这个本地仓库进行修改，之后commit即可。具体步骤如下：
   1. 以xuexi仓库为例，进入远程仓库，选择Clone or download，复制仓库地址。
   2. 在本地自定义一个文件夹来创建仓库，如：/Users/noodles_bo/Documents/Gitrepo
   3. 先cd到此目录中：cd ~/Documents/Gitrepo，然后输入命令将远程仓库clone到本地：git clone https://github.com/Anguswin/xuexi.git
   4. 此时在本地已经看到clone了远程仓库，然后