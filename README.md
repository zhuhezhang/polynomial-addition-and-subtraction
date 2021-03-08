﻿@[TOC](目录)
# 1.题目
【问题描述】
      设计一个一元稀疏多项式简单计算器。 
【基本要求】
     （1）输入并建立两个多项式；
     （2）多项式a与b相加，建立和多项式c；
     （3）多项式a与b相减，建立差多项式d；
     （4）输出多项式a, b, c, d。输出格式：比如多项式a为：A(x)=c1xe1+ c2xe2+…+ cmxem，其中，ci和ei分别为第i项的系数和指数，且各项按指数的升幂排列，即0≤e1＜e2＜…＜em。
【测试数据】
    （1）(1+x+x2+x3+x4+x5)+(-x3-x4)=(1+x+x2+x5)
    （2）(x+x100)+(x100+x200)=(x+2x100+x200)
    （3）(2x+5x8-3x11)+(7-5x8+11x9)=(7+2x+11x9-3x11)
    （4）(6-x+4.4x2-1.2x9)-(-6+4.4x2+7.8x15)=(12-x-1.2x9-7.8x15)
【实现提示】
    （1）用带头结点的单链表存储多项式。
    （2）每个多项式链表中都只存储非零系数项。若多项式a与b中指数相等的两项相加/减后，系数为零，则在和/差多项式中不存储该指数项。 
【拓展内容】
计算器的仿真界面。
# 2.需求分析
本程序需要实现运用单链表按指数从小到大输入两个一元多项式并进行加或减，结果系数为零的不存储、不输出，且最后结果也是按指数从小到大输出的功能。
# 3.程序设计
本程序代码分三个文件，其中第一个文件是利用一个结构体来存储数据以及一个类来声明相关操作函数，第二个文件是类里面的函数的具体实现代码，包括建立链表函数、执行函数以及多项式相加减函数，而第三个文件则是主函数调用。
首先介绍的是结构体以及类的定义部分：结构体里吃了包含多项书的系数、指数以及指针link外，还有Data构造函数以及一个插入结点函数（创建链表函数）。类Polynomal里面的public含有其构造函数，其功能是创建一个Data头结点；还有一个取Data的指针first；接下来是执行函数、以及多项式加减函数；而private只有一个指针Data* first。
接下来是类里面函数的代码实现的文件：首先是插入新节点的函数，使用new分配内存，调用Data构造函数，最后返回link指针。至于执行函数，首先时一个修改运行时的字体颜色的代码（无聊时弄的，同时字体颜色突出也是为了提醒使用者吧），在windows.h头文件中定义，为了实现多次对多项式的加减，接下来的代码包含在一个while循环中，在循环后面利用if语句判断是否继续执行，若不执行则调用break语句退出该大循环。循环里面首先是各个变量的定义以及初始化，然后就是分别输入AB多项式并利用insert函数插入链表中，然后就是输入指令并输出计算结果，1则作加法，2则做减法，输入其他则发出错误指令并提示重输入指令并利用continue语句再次进行条件判断，大循环后也就是前面说的是否继续执行操作。
最后一部分是对多项式的相加减函数，由于两者算法差别不大，所以这里只说明加法的：同样的前面还是各个变量的定义，然后使Data类型的指针pa、pb分别指向多项式A、B的头结点，然后while(pa!=nullptr && pb!=nullptr)时执行计算，分三种情况：当pb指数小时，调用insert将pb对应的结点插入C多项式中，并将pb指针完后移，若pa的小，则进行类似的操作，当两者指数相同时，则将他们相加并插入C中，然后pa、pb指针都往后移。然后就处理A或B剩余的部分，直接调用insert将剩余部分插入至C中，最后返回C，至此，算法结束。
最后是主函数文件了，直接定义一个对象A调用执行函数Execute执行就好。
# 4.测试结果
测试结果如下图所示：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210308152209484.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNzk0NjMz,size_16,color_FFFFFF,t_70#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/2021030815221777.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQzNzk0NjMz,size_16,color_FFFFFF,t_70#pic_center)