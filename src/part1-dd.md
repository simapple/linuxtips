dd 备份命令
==========
###dd 是一个命令 用于改变和复制文件
在unix上，设备驱动器向硬盘或者其他的设备比如 /dev/null /dev/random 这些出现在文件系统的
东西都被认为是一般文件。dd 能够操作这些文件，比如进行文件备份 修复文件数据。同时dd还能转化文件格式

dd 的语法格式 使用 选项=值 的方式，dd 从 STDIN 中读，向 STDOUT 写入，他们分别可以使用 if 和of来代替


区块大小
一个区块就是一组bytes，他们被用来作为读 写 转化的基本元素。命令中可以指定不同的大小来读和写。。一般系统默认的是512bytes。为了让读写更高效，在使用dd的时候可以设定一个好用区块大小。比如在一块硬盘上做数据操作的时候，更小的区块大小，意味着更多的读写和转化操作。

（跳过不同区块大小的计算）

使用方式

数据传输
dd可以跨文件，设备，分区，量来复制数据。在复制的过程中可以使用conv项来控制介质。特别是在有些时候，cp 命令在数据结束字节上有问题的时候，会失败，而dd却能成功复制。

示例：
主启动记录备份
复制软盘的前2个扇形区内容
dd if=/dev/fd0 of=MBRboot.img bs=512 count=2
复制x86 启动镜像
dd if=/dev/sda of=MBR.img bs=512 count=1
复制出启动镜像，不包含分区表和魔术字节
dd if=/dev/sda of=MBR_boot.img bs=446 count=1

修改数据
用空字节复写文件的前512bytes
dd if=/dev/zero of=path/to/file bs=512 count=1 conv=notrunc
（notrunc 表示只替换不创建）
将文件分区修改为分区镜像
dd if=/dev/sdb2 of=partition.image bs=4096 conv=noerror

数据擦除
检查数据是否存在 发送输出到标准输出
dd if=/dev/sda
使用zeros擦除数据
dd if=/dev/zero of=/dev/sda bs=4k conv=notrunc
（使用zero的一些有点就不复述了）
数据恢复
（建议使用不同os上定制的数据恢复软件）
驱动器性能测试
dd if=/dev/zero bs=1024 count=1000000 of=file_1GB
dd if=file_1GB of=/dev/null bs=1024
生成随机数据文件
dd if=/dev/urandom of=myrandom bs=100 count=1
创建任意大小的空文件
dd if=/dev/zero of=mytestfile.out bs=1 count=0 seek=1G


##总结 总的来说这个命令是一个操作数据的好命令 能够方便操作文件字节
[linux dd命令](http://www.simapple.com/242.html "linux dd命令")
