### 基本的bash shell命令
1. man命令用力啊访问存储在Linux系统上的手册页面，在想要查找的工具的名称前面输入man命令，就可以找到那个工具对应的手册条目。
	eg. man xterm
2. ls -a（显示隐藏文件） -F（区分文件类型） -R（递归选项） -l（长列表）
3. touch flie_name 创建文件
4. cp -i(提示是否覆盖已有文件) source destination(若为文件名，则复制文件) 复制文件到制定路径下
5. 单点符(.)表示当前路径，双点符(..)表示父目录
6. mv source destination 重命名或者移动文件
7. mkdir New_Dir 创建目录
   rmdir (-ri先进入子目录，删除其中的文件后在删除目录本身)(-rf强制删除目录及其内容) New_Dir 删除目录 默认只允许删除空文件夹
8. file file_name 查看文件类型
   cat (-n)(-b) file_name 查看文件内容
9. more file_name 分页查看文件内容，空格/回车前进
10. tail (-n 2) file_name 查看文件最后(2)n行内容
	head (-5) file_name 查看文件开头(5)行内容


### 更多的bash shell命令
1. 查看进程
	默认情况下，ps只会显示运行在当前控制台下的属于当前用户的进程。
	Unix风格的参数 -efl 显示所有进程，显示长进程信息
	BSD风格的参数 l 显示进程的信息， STAT列能输出更详细的状态进程码
	GNU长参数 --forest 用层级结构显示出进程和父进程之间的关系
2. 实时监测进程
	top能够显示进程信息，但它是实时显示的
3. 结束进程
	kill 命令通过及昵称ID(PID)给进程发信号。
	killall 支持通过进程名而不是PID来结束进程
4. 挂载存储媒体
	mount 默认情况下，mount命令会输出当前系统上挂载的设备列表
	手动挂载媒体设备的基本命令：mount -t type device directory eg. mount -t vfat dev/sdb1 /media/disk
	卸载设备的命令： umount [directory | device]  eg.安装和弹出u盘时使用
5. 查看设备磁盘空间
	df命令可以查看所有已挂载磁盘的使用情况
	du命令可以显示某个特定目录（默认情况下是当前目录）的磁盘使用情况。 -h -s
6. 处理数据文件
	sort (-n 按数字数值排序) (-M 按月份排序) file_name
	grep (-v 反向搜索) (-n 显示行号) (-c 显示匹配行数) (-e 可用于制定多个匹配模式) pattern [file] 在文件中查找匹配pattern的内容
	gzip file_name 压缩制定的文件
	tar function [options] object1 object2... tar 命令是给整个目录结构创建归档文件的简便方法。 tar -zxvf filename.tgz可用于解压


###理解shell
1. shell的父子关系
	可以在bash中输入bash命令，产生bash的子进程并进入子进程，通过ps --forest可以查看父子进程之间的层次关系，使用exit退出子进程
2. 进程列表
	(pwd; ls; de /etc; pwd; cd; pwd; ls) 把命令列表放在括号里就构成进程列表，生成了一个子shell来执行对应的命令。产生子shell会明显拖慢处理速度。命令执行完之后会返回父shell
	(pwd; ls; de /etc; pwd; cd; pwd; ls; echo $BASH_SUBSHELL) 会返回产生子shell的个数（是否产生子shell）
3. 后台模式
	sleep 60& 把进程置入后台（睡眠60秒）
	jobs 用于显示后台作业信息