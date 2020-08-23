# 一个实用的代码查重工具——sim
* sim工具可用于搭建在线OJ平台，用于检测网络比赛中代码复制粘贴的现象，是一个轻量化的代码查重工具。
## 安装配置
* 下载解包之后查看并编辑Makefile的配置，进行编译，步骤如下：
  * 选择操作系统，Makefile里有两套配置，一套是“For UNIX-like systems”，另一套是“For MSDOS + MinGW”，根据当前系统把另一套注释掉就行了。
  * 修改BINDIR的值，推荐设置为/usr/bin/，一般来说，放到$PATH下比较方便。
  * 修改MAN1DIR的值，推荐设置为/usr/share/man/man1，这个目录是系统man文档的默认目录。
  * 将sim.1文件放到刚才设置的MAN1DIR里，放进去之后，man sim命令就应该可用了。
  * 安装依赖，一般来说，安装了gcc,make,flex这几个东西就够了。
  * 执行make install。

搞定之后就会发现生成了可执行文件:
```
sim_8086
sim_c
sim_c++
sim_java
sim_lisp
sim_m2
sim_mira
sim_pasc
sim_txt
```
这样，编译工作就搞定了。

> 特别的，对于windows用户，我们提供了编译完成的可执行文件，您可以在仓库的bin文件夹中下载，或在https://github.com/aspxcor/Code-Repetition-Check-sim/releases 中获得适用于windows版本的可执行文件

## 用法
* 选择语言： sim 支持多种语言：C, Java, Pascal, Modula-2, Lisp , Miranda, or text files，对应的命令分别是： sim_c ，sim_java，sim_pasc ，sim_m2，sim_lisp ，sim_mira，sim_text 。
* 选择参数： 常用的参数有三个：
	
参数 | 含义
:-: | :-: 
-p | 表示以“F consists for x % of G material”的形式输出相似度| 
-t N | 表示只显示相似度大于N%的条目（除text 默认为20%外，其余默认为1%);|
-o file | 表示将结果输出到file中|

    最后可以输入文件名，支持通配符。
## 文件说明
**sim_bin**	Windows可执行文件

**sim_src**	源文件
## 示例
*如下两个文件：
```cpp
//a.cpp
#include<stdio.h>
typedef struct //定义一个新的数据类型
{
	int yue;//月份
	int tian;//天
}Date;
void f(Date x, Date y);//函数声明
int main()
{
	Date date1, date2;
	//类型赋值
	printf("输入一个日期（mm/dd）：\n");
	scanf_s("%d/%d", &date1.yue, &date1.tian);
	printf("再输入一个日期（在上一个日期之后）（mm/dd）：\n");
	scanf_s("%d/%d", &date2.yue, &date2.tian);
	//调用函数
	f(date1, date2);
	return 0;
}
void f(Date x, Date y)
{
	int m, n;
	int t;
	//计算两个日期的天数
	switch (x.yue)
	{
	case 1:m = x.tian; break;
	case 2:m = x.tian + 31; break;
	case 3:m = x.tian + 59; break;
	case 4:m = x.tian + 90; break;
	case 5:m = x.tian + 120; break;
	case 6:m = x.tian + 151; break;
	case 7:m = x.tian + 181; break;
	case 8:m = x.tian + 212; break;
	case 9:m = x.tian + 243; break;
	case 10:m = x.tian + 273; break;
	case 11:m = x.tian + 304; break;
	case 12:m = x.tian + 334; break;
	}
	switch (y.yue)
	{
	case 1:n = y.tian; break;
	case 2:n = y.tian + 31; break;
	case 3:n = y.tian + 59; break;
	case 4:n = y.tian + 90; break;
	case 5:n = y.tian + 120; break;
	case 6:n = y.tian + 151; break;
	case 7:n = y.tian + 181; break;
	case 8:n = y.tian + 212; break;
	case 9:n = y.tian + 243; break;
	case 10:n = y.tian + 273; break;
	case 11:n = y.tian + 304; break;
	case 12:n = y.tian + 334; break;
	}
	//求相差天数
	t = n - m;
	printf("相差的天数：%d\n", t);
}
```


```cpp
//b.cpp
#include<stdio.h>
typedef struct //使用结构体
{
	int month;
	int day;
}date;
int f(date d1, date d2);//函数声明
int main(void)
{
	date d1, d2;
	printf("输入第一个日期:\n");
	scanf_s("%d,%d", &d1.month, &d1.day);//输入第一个日期
	printf("输入第一个日期:\n");
	scanf_s("%d,%d", &d2.month, &d2.day);//输入第二个日期
	printf("相差%d天", f(d1, d2));//调用函数并输出相差天数
	return 0;
}
int f(date d1, date d2)//函数定义
{
	int x, m, n;
	switch (d1.month)//计算第一个日期是一年的第几天
	{
	case 1:
		m = d1.day;break;
	case 2:
		m = d1.day + 31;break;
	case 3:
		m = d1.day + 59;break;
	case 4:
		m = d1.day + 90;break;
	case 5:
		m = d1.day + 120;break;
	case 6:
		m = d1.day + 151;break;
	case 7:
		m = d1.day + 181;break;
	case 8:
		m = d1.day + 212;break;
	case 9:
		m = d1.day + 243;break;
	case 10:
		m = d1.day + 273;break;
	case 11:
		m = d1.day + 304;break;
	case 12:
		m = d1.day + 334;break;
	}
	switch (d2.month)//计算第二个日期是一年的第几天
	{
	case 1:
		n = d2.day;break;
	case 2:
		n = d2.day + 31;break;
	case 3:
		n = d2.day + 59;break;
	case 4:
		n = d2.day + 90;break;
	case 5:
		n = d2.day + 120;break;
	case 6:
		n = d2.day + 151;break;
	case 7:
		n = d2.day + 181;break;
	case 8:
		n = d2.day + 212;break;
	case 9:
		n = d2.day + 243;break;
	case 10:
		n = d2.day + 273;break;
	case 11:
		n = d2.day + 304;break;
	case 12:
		n = d2.day + 334;break;
	}
	x = m - n;//计算日期差
	if (x >= 0)//返回非负值
		return x;
	else
		return -x;
}
```

这两个是用来计算日期差的cpp文件，虽然看上去有差别，且很多变量名都经过了替换，修改了注释，也改了缩进的风格，但是经过sim程序判别之后，可以发现他们的相似度还是极高的：

```
ponyding@Business:~/桌面$ sim_c -p a.cpp b.cpp
File a.cpp: 374 tokens, 82 lines
File b.cpp: 388 tokens, 81 lines
Total: 762 tokens

a.cpp consists for 89 % of b.cpp material
b.cpp consists for 86 % of a.cpp material
```

相似度仍然达到了90%左右，所以我们可以确定的认为这两份代码存在抄袭。
