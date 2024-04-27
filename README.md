# -
写的第一个github项目，介绍一下csapp里面关于fork（）的运用与命令pstree -p吧

以下命令适用于linux学习：

学习ps、pstree和kill等命令的使用方法。能通过ps命令查看进程号、可执行文件名（命令）、运行状态信息；能通过pstree查看系统进程树；能利用kill命令根据进程号（pid）杀死进程。

"gcc 创建的代码名字 -o hello" 用于编译  "./hello &"用于执行（&表示后台执行，运行后会出现父进程pid）

.在lab6文件夹里面编写代码，创建6个子进程，并保存为2.c

编写3.c，实现6层子进程嵌套（使用getchar作为阻塞，子进程会被kill且ps只能显示2个进程，此处选用pause阻塞）

编写4.c，实现一个父进程下面3个子进程，一个子进程下面3个进程。

编写5.c，实现父进程与子进程交替输出10次，父进程输出word pid，子进程输出 hello pid。

自定义shell
尝试自行设计一个C语言小程序，完成基本的shell功能


2.c参考代码
#include<stdio.h>
#include<unistd.h>
int main()
{
	for(int i=0;i<6;i++)
	{
		pid_t pid =fork();
		if(pid<0) printf("error!");
		if(pid==0)	break;
		if(pid>0)       continue;
	}
	getchar();
	return 0;
}


如果pstree -apu 20359 的输出仍然不完整，您可以尝试使用 -h 选项来禁止截断输出

补充：
pstree命令是用于查看进程树之间的关系，即哪个进程是父进程，哪个是子进程，可以清楚的看出来是谁创建了谁
#pstree
几个重要的参数：
-A: 各进程树之间的连接以ASCII码字符来连接
-U:各进程树之间的连接以utf8字符来连接，某些终端可能会有错误
-p:同时列出每个进程的PID
-u: 同时列出每个进程的所属账号名称：
