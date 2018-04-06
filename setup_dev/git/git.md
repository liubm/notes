1. 安装git
yum install git

2. git 基本设置
1.1 设置用户名
  git config --global user.name "liubm"
2.2 设置邮箱
  git config --global user.email "liubm16@163.com"
2.3 查看git设置
  git config -l

3. 初始化仓库
  git init

4 提交新文件到仓库
   echo "Hello World " > test.md
   git status
   git add test.md
   git status
   git commit -m "add test.md"
   git status

5. 克隆仓库到本地
   git clone https://github.com/liubm/notes.git
6. 提交本地仓库到远程仓库
   6.1 设置用户密码 vim .git/config  
   6.2 同步到远程仓库 
	git push
