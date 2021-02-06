# Ubuntu

## 删除软件

### 如果你知道要删除软件的具体名称，可以使用

`sudo apt-get remove --purge 软件名称`
`sudo apt-get autoremove --purge 软件名称`

### 如果不知道要删除软件的具体名称，可以使用

`dpkg \-\-get\-selections \| grep ‘软件相关名称’`

`sudo apt-get purge 一个带core的package，如果没有带core的package，则是情况而定。`

## 清理残留数据

`dpkg \-l \|grep ^rc\|awk '\{print $2\}' \|sudo xargs dpkg \-P`

## 列出内核

### 列出当前使用内核

`uname -r`

### 列出所有内核

`dpkg \-\-get\-selections \| grep linux`

## 新立得恢复搜索栏

`sudo apt-get install apt-xapian-index`
`sudo update-apt-xapian-index`

# Archlinux

## 使用Goagent代理全局在配置文件中加入

export http\_proxy=http://127.0.0.1:8087/

export https\_proxy=$http\_proxy

export HTTP\_PROXY=$http\_proxy

export HTTPS\_PROXY=$HTTP\_PROXY

## fcitx无法使用，在.xinitrc和.xprofile加入

export GTK\_IM\_MODULE=fcitx

export QT\_IM\_MODULE=fcitx

export XMODIFIERS="@im=fcitx"

## 一个或多个pgp签名无法验证

gpg --recv-keys xxxxxxxx

## 自动挂载

编辑/usr/share/polkit-1/actions/org.freedesktop.udisks2.policy
把与id="org.freedesktop.udisks2.filesystem-mount-system"对应的
<allow\_active>auth\_admin\_keep</allow\_active>改为
<allow\_active>yes</allow\_active>

## grub修复

1. grub>root

//看看所在boot分区，可能返回 hd(0,1),那么你台式机一般是/dev/hda1,笔记本一般是/dev/sda1, 现在假设是sda1

2. grub>linux /boot/vmlinuz(按tab键自动补全) /dev/sda1

//补全后好象是vmlinuz-2.6.**-**-generic记不清楚了

```

```

3. grub>initrd /boot/initrd(tab键自动补全)
4. grub>boot 启动
5. 进入ubuntu，终端输入 update-grub2

## livecd修复grub

1.首先挂载根目录

sudo su
mount /dev/sdb1 /mnt

2.接下来将一些需要的目录“绑定到” live CD的系统上去

mount --bind /dev /mnt/dev
mount --bind /proc /mnt/proc
mount --bind /sys /mnt/sys

3.最后切换root根目录到/mnt

chroot /mnt

4.这样我们就切换回我们原来的系统上了， 执行update-grub来更新引导

sudo update-grub

不出意外的话重启就能进入系统了 ， 整个过程如下图
