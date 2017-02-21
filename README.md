# Ubuntu-
1、删除软件

方法一、如果你知道要删除软件的具体名称，可以使用               

sudo apt-get remove --purge 软件名称 
sudo apt-get autoremove --purge 软件名称 

方法二、如果不知道要删除软件的具体名称，可以使用

dpkg --get-selections | grep ‘软件相关名称’

sudo apt-get purge 一个带core的package，如果没有带core的package，则是情况而定。

2、清理残留数据

dpkg -l |grep ^rc|awk '{print $2}' |sudo xargs dpkg -P  

3.列出当前使用内核
uname  -r

4.列出所有内核
dpkg --get-selections | grep linux
Archlinux
---------

 1. 使用Goagent代理全局在配置文件中加入

 export http_proxy=http://127.0.0.1:8087/
 
 export https_proxy=$http_proxy
 
 export HTTP_PROXY=$http_proxy
 
 export HTTPS_PROXY=$HTTP_PROXY

 2. fcitx无法使用

 export GTK_IM_MODULE=fcitx
 
 export QT_IM_MODULE=fcitx
 
 export XMODIFIERS="@im=fcitx"
 

 3. 一个或多个pgp签名无法验证

 gpg --recv-keys xxxxxxxx
