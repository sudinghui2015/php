##  git安装
```txt
下载git客户端，下载地址为：https://git-scm.com/download/mac
```
##  创建ssh&github添加密钥
```txt
*打开终端
 cd ~/.ssh
*生成sshkey
ssh-keygen -t rsa -C 511524899@qq.com
*进入.ssh目录并cat id_rsa.pub
*将id_rsa.pub内容拷贝到github密钥
```
##  本地关联远端仓库
```txt
*在指定本地文件夹处：git init
*git clone <远端git>
*git pull
```
