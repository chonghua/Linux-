# Ubuntu
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

5.新立得恢复搜索栏
sudo apt-get install apt-xapian-index
sudo update-apt-xapian-index


Archlinux
---------

 1. 使用Goagent代理全局在配置文件中加入

 export http_proxy=http://127.0.0.1:8087/
 
 export https_proxy=$http_proxy
 
 export HTTP_PROXY=$http_proxy
 
 export HTTPS_PROXY=$HTTP_PROXY

 2. fcitx无法使用，在.xinitrc和.xprofile加入
 export GTK_IM_MODULE=fcitx
 
 export QT_IM_MODULE=fcitx
 
 export XMODIFIERS="@im=fcitx"
 

 3. 一个或多个pgp签名无法验证

 gpg --recv-keys xxxxxxxx
 
 自动挂载
 编辑/usr/share/polkit-1/actions/org.freedesktop.udisks2.policy
把与id="org.freedesktop.udisks2.filesystem-mount-system"对应的
<allow_active>auth_admin_keep</allow_active>改为
<allow_active>yes</allow_active>


**grub修复**

 1. grub>root

  //看看所在boot分区，可能返回 hd(0,1),那么你台式机一般是/dev/hda1,笔记本一般是/dev/sda1, 现在假设是sda1

 2. grub>linux /boot/vmlinuz(按tab键自动补全) /dev/sda1

   //补全后好象是vmlinuz-2.6.**-**-generic记不清楚了

 3. grub>initrd /boot/initrd(tab键自动补全)

 4. grub>boot 启动

 5. 进入ubuntu，终端输入 update-grub2
 
 **livecd修复grub**
 
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

#字体配置文件fonts.conf
 <?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
    <match target="font">
        <edit name="antialias" mode="assign">
            <bool>true</bool>
        </edit>
        <edit name="hinting" mode="assign">
            <bool>true</bool>
        </edit>
        <edit name="hintstyle" mode="assign">
            <const>hintfull</const>
        </edit>
        <edit name="rgba" mode="assign">
            <const>rgb</const>
        </edit>
        <edit name="autohint" mode="assign">
            <bool>false</bool>
        </edit>
        <edit name="lcdfilter" mode="assign">
            <const>lcddefault</const>
        </edit>
        <edit name="dpi" mode="assign">
            <double>102</double>
        </edit>
    </match>
    <!-- Default fonts - Linux Appearance -->
	<alias>
		<family>sans-serif</family>
		<prefer>
			<family>Microsoft YaHei</family>
		</prefer>
	</alias>
	<alias>
		<family>serif</family>
		<prefer>
			<family>SimSun</family>
		</prefer>
	</alias>
	<alias>
		<family>monospace</family>
		<prefer>
			<family>Courier New</family>
		</prefer>
	</alias>
		<alias>
		<family>Roboto</family>
		<prefer>
			<family>Arial</family>
		</prefer>
	</alias>

	<match target="pattern">
		<test name="family">
			<string>Cantarell</string>
		</test>
		<edit name="family" mode="assign" binding="strong">
			<string>Cantarell</string>
		</edit>
	</match>

	<match target="font">
		<test name="do_substitutions">
			<bool>true</bool>
		</test>
		<test name="family">
			<string>serif</string>
		</test>
		<edit name="family" mode="assign">
			<string>Times New Roman</string>
		</edit>
	</match>
	<match target="font">
		<test name="do_substitutions">
			<bool>true</bool>
		</test>
		<test name="family">
			<string>monospace</string>
		</test>
		<edit name="family" mode="assign">
			<string>Courier New</string>
		</edit>
	</match>

	<match target="font">
		<test name="do_substitutions">
			<bool>true</bool>
		</test>
		<test name="family">
			<string>Roboto Mono</string>
		</test>
		<edit name="family" mode="assign">
			<string>Courier New</string>
		</edit>
	</match>
	
	<match target="font">
		<test name="do_substitutions">
			<bool>true</bool>
		</test>
		<test name="family">
			<string>Roboto</string>
		</test>
		<edit name="family" mode="assign">
			<string>Arial</string>
		</edit>
	</match>

	<match target="font">
		<test name="do_substitutions">
			<bool>true</bool>
		</test>
		<test name="family">
			<string>Roboto Mono</string>
		</test>
		<edit name="family" mode="assign">
			<string>Arial</string>
		</edit>
	</match>

	<match target="font">
		<test name="do_substitutions">
			<bool>true</bool>
		</test>
		<test name="family">
			<string>Slack-Lato</string>
		</test>
		<edit name="family" mode="assign">
			<string>Courier New</string>
		</edit>
	</match>

	<match target="font">
		<test name="slant">
			<const>roman</const>
		</test>
		<test target="pattern" name="slant" compare="not_eq">
			<const>roman</const>
		</test>
		<test name="scalable">
			<bool>false</bool>
		</test>
		<edit name="slant" mode="assign">
			<const>oblique</const>
		</edit>
	</match>
	
	<match target="font">
		<test name="weight" compare="less_eq">
			<const>medium</const>
		</test>
		<test target="pattern" name="weight" compare="more">
			<const>medium</const>
		</test>
		<test name="scalable">
			<bool>false</bool>
		</test>
		<edit name="weight" mode="assign">
			<const>bold</const>
		</edit>
	</match>
	
	<!-- Prevent bold-ish fonts from being emboldened -->
	<match target="font">
		<test name="weight" compare="more_eq">
			<const>semibold</const>
		</test>
		<test target="pattern" name="weight">
			<const>bold</const>
		</test>
		<edit name="weight" mode="assign">
			<const>bold</const>
		</edit>
	</match>

	<!-- Prevent thin-ish fonts from being emboldened -->
	<match target="font">
		<test name="weight" compare="less">
			<const>book</const>
		</test>
		<test target="pattern" name="weight">
			<const>bold</const>
		</test>
		<edit name="weight" mode="assign">
			<const>bold</const>
		</edit>
	</match>
	
	<match target="pattern">
		<test target="font" name="family">
			<string>f</string>
		</test>

		<!-- match requests for non-roman face -->
		<test name="slant" compare="not_eq">
			<const>roman</const>
		</test>

		<!-- remember that this should be slanted -->
		<edit name="fake_slant" mode="assign">
			<bool>true</bool>
		</edit>

		<!--- change to match a roman face instead -->
		<edit name="slant" mode="assign">
			<const>roman</const>
		</edit>
	</match>

	<!-- Force flagged fonts to have artificial oblique -->
	<match target="font">
		<!-- check to see if the font is roman -->
		<test name="slant">
			<const>roman</const>
		</test>
		<!-- look for fonts which were marked for fake obliquing -->
		<test name="fake_slant">
			<bool>true</bool>
		</test>
		<!-- multiply the matrix to slant the font -->
		<edit name="matrix" mode="assign">
			<times>
				<name>matrix</name>
				<matrix>
					<double>1.0</double>
					<double>0.2</double>
					<double>0</double>
					<double>1</double>
				</matrix>
			</times>
		</edit>
		<!-- pretend the font is oblique now -->
		<edit name="slant" mode="assign">
			<const>oblique</const>
		</edit>
	</match>


	<!-- Force fake bold instead of the font's default bold -->
	<!-- In rare cases this is more visually appealing -->
	<!-- !!!! Somehow this breaks Qt unfortunately !!!! -->
	<!-- Set the flag -->
	<match target="pattern">
		<test name="family">
			<string>Courier New</string>
		</test>

		<!-- match requests for bold face -->
		<test name="weight" compare="more">
			<const>medium</const>
		</test>

		<!-- remember that this should be bolded -->
		<edit name="fake_bold" mode="assign">
			<bool>true</bool>
		</edit>

		<!--- change to match a medium weight instead -->
		<edit name="weight" mode="assign">
			<const>medium</const>
		</edit>
	</match>

	<!-- Force flagged fonts to have artificial bold -->
	<match target="font">
		<!-- look for fonts which were marked for fake bolding -->
		<test name="fake_bold">
			<bool>true</bool>
		</test>
		<!-- Set the embolden flag -->
		<edit name="embolden" mode="assign">
				<bool>true</bool>
		</edit>
		<!-- pretend the font is bold now -->
		<edit name="weight" mode="assign">
			<const>bold</const>
		</edit>
	</match>
	<match target="pattern">
		<test name="family">
			<string>Lucida Grande</string>
		</test>
		<test name="pixelsize" compare="eq">
			<double>9</double>
		</test>
		<edit name="family" mode="prepend" binding="same">
			<string>Arial</string>
		</edit>
	</match>

	<match target="pattern">
    	<test qual="any" name="family"><string>Consolas</string></test>
    		<edit name="family" mode="assign" binding="same"><string>Courier New</string>
    	</edit>
  	</match>

  	<match target="pattern">
    	<test qual="any" name="family"><string>Segoe UI</string></test>
    		<edit name="family" mode="assign" binding="same"><string>Arial</string>
    	</edit>
  	</match>
  	
  	<match target="pattern">
    	<test qual="any" name="family"><string>Roboto</string></test>
    		<edit name="family" mode="assign" binding="same"><string>Arial</string>
    	</edit>
  	</match>

  	 <match target="pattern">
    	<test qual="any" name="family"><string>Noto Sans</string></test>
    		<edit name="family" mode="assign" binding="same"><string>Arial</string>
    	</edit>
  	</match>

  	<match target="pattern">
    	<test qual="any" name="family"><string>Helvetica</string></test>
    		<edit name="family" mode="assign" binding="same"><string>Arial</string>
    	</edit>
  	</match>

  	<match target="pattern">
    	<test qual="any" name="family"><string>Helvetica Neue</string></test>
    		<edit name="family" mode="assign" binding="same"><string>Arial</string>
    	</edit>
  	</match>

  	  	<match target="pattern">
    	<test qual="any" name="family"><string>"Helvetica Neue"</string></test>
    		<edit name="family" mode="assign" binding="same"><string>Arial</string>
    	</edit>
  	</match>

  	<match target="pattern">
    	<test qual="any" name="family"><string>proxima-nova</string></test>
    		<edit name="family" mode="assign" binding="same"><string>Arial</string>
    	</edit>
  	</match>

  	  	<match target="pattern">
    	<test qual="any" name="family"><string>"proxima-nova"</string></test>
    		<edit name="family" mode="assign" binding="same"><string>Arial</string>
    	</edit>
  	</match>

  	<match target="pattern">
    	<test qual="any" name="family"><string>Source Code Pro</string></test>
    		<edit name="family" mode="assign" binding="same"><string>Courier New</string>
    	</edit>
  	</match>

  	<match target="pattern">
    	<test qual="any" name="family"><string>sans-serif</string></test>
    		<edit name="family" mode="assign" binding="same"><string>Arial</string>
    	</edit>
  	</match>

  	<match target="pattern">
    	<test qual="any" name="family"><string>Roboto Mono</string></test>
    		<edit name="family" mode="assign" binding="same"><string>Courier New</string>
    	</edit>
  	</match>  	

  	<match target="pattern">
    	<test qual="any" name="family"><string>Roboto</string></test>
    		<edit name="family" mode="assign" binding="same"><string>Arial</string>
    	</edit>
  	</match>  	

  	<match target="pattern">
    	<test qual="any" name="family"><string>RobotoDraft</string></test>
    		<edit name="family" mode="assign" binding="same"><string>Arial</string>
    	</edit>
  	</match>  
  	  
  		<!-- These full hinted fonts should use slight hinting below 12 px -->
	<match target="font">
		<test name="family">
			<string>Arial Black</string>
		</test>
		<test name="pixelsize" compare="less">
			<double>12</double>
		</test>
		<edit name="hintstyle" mode="assign">
			<const>hintslight</const>
		</edit>
		<edit name="autohint" mode="assign">
			<bool>true</bool>
		</edit>
	</match>
	
		<!-- Inconsolata-Bold.otf looks like crap -->
	<selectfont>
		<rejectfont>
			<pattern>
				<patelt name="family" >
					<string>Inconsolata</string>
				</patelt>
				<patelt name="weight" >
					<const>bold</const>
				</patelt>
			</pattern>
		</rejectfont>
	</selectfont>

</fontconfig>
