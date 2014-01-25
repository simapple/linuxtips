使用grub2 命令 启动linux
=========================
今天安装了一个linux虚拟机，一时疏忽安装了grub但是忘记了，创建grub.cfg
启动系统直接进入了grub命令模式，再次挂载生成比较费时间，就找了一下grub2的文档
grub2 和grub还是有一些区别的
启动linux 是要指定linux 内核，已经root的所在位置

linux /boot/kernel-0125 root=/dev/sda3

这个命令就是指明要启动linux内核和root分区
我的内核文件是 /boot/kernel-0125 root 挂载 /dev/sda3 分区

然后执行

boot

这样就可以引导启动linux了
然后生成grub的配置文件
grub-mkconfig >> /boot/grub/grub.cfg

重启一切正常

详细访问：http://www.simapple.com
