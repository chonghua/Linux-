# Linux-
1、删除软件

方法一、如果你知道要删除软件的具体名称，可以使用               

sudo apt-get remove --purge 软件名称 
sudo apt-get autoremove --purge 软件名称 

方法二、如果不知道要删除软件的具体名称，可以使用

dpkg --get-selections | grep ‘软件相关名称’

sudo apt-get purge 一个带core的package，如果没有带core的package，则是情况而定。

2、清理残留数据

dpkg -l |grep ^rc|awk '{print $2}' |sudo xargs dpkg -P  
