## 🚀 《C语言》游戏开发基础
+ **游戏框架搭建**
  ```c
  // 函数外全局变量定义

  int main()
  {
      startup();  // 数据初始化
      while (1) //  游戏循环执行
      {
          show();  // 显示画面
          updateWithoutInput();  // 与用户输入无关的更新
          updateWithInput();  // 与用户输入有关的更新
      }
      return 0;
  }
  ```
## 目录
  ***功能性***
  1. [清屏函数](#1)
  
  1. [延时函数](#2)
  
  1. [停止等待函数](#3)
  
  1. [系统自带发出铃声](#4)
  
  1. [读取键盘上输入的值(需要回车)](#5)
  
  1. [读取键盘上输入的值(不需要回车)](#6)
  
  1. [判断是否有键盘输入的函数](#7)
  
  1. [产生随机数的函数](#8)
  
  1. [光标移动到原点位置进行重画(实现类似于清屏函数的效果)](#9)
  
  1. [隐藏光标显示函数](#10)
  
  1. [添加背景音乐](#21)
  
  1. [计时函数](#22)
  
  ***窗口***
  1. [修改窗口大小(静态)](#11)
  
  1. [修改窗口大小(动态)](#12) 
  
  1. [固定窗口大小](#13)
  
  1. [修改窗体风格](#14)
  
  1. [设置指定窗口的显示状态](#15)
  
  1. [修改窗口标题](#16)
  
  1. [弹出消息框](#17)
  
  1. [修改字体颜色、背景颜色 ](#18)
  
  1. [修改文本颜色](#19)
  
  1. [修改窗体icon图标](#20)
  
  1. [修改窗体透明度](#23)
  
  <a name="1"></a>
+ **清屏函数**
  ```c
  #include <stdlib.h>
  system("cls");
  ```
  <a name="2"></a>
+ **延时函数**
  ```c
  #include <windows.h>
  Sleep(20);    //其中20的单位为毫秒
  ```
  <a name="3"></a>
+ **停止等待函数**
  ```c
  #include <windows.h>
  system("pause");
  ```
  <a name="4"></a>
+ **系统自带发出铃声**
  ```c
  printf("\a");
  ```
  <a name="5"></a>
+ **读取键盘上输入的值(需要回车)**
  ```c
  char input;
  scanf("%c",&input);
  if(input=='w')
      printf("w");
  ```
  <a name="6"></a>
+ **读取键盘上输入的值(不需要回车)**
  ```c
  #include<conio.h>
  
  char input;
  //scanf("%c",&input);
  input = getch();
  if(input=='w')
      printf("w");
  ```
  <a name="7"></a>
+ **判断是否有键盘输入的函数**
  ```c
  #include <conio.h>
  kbhit();   //若有则返回一个非0值，否则返回0
  ```
  > 示例：
  ```c
  #include <stdio.h>
  #include <conio.h>

  int main()
  {
      char input;
      if(kbhit()){
          scanf("%c",&input);    //需要按下回车键来读取
          //input=getch();
          printf("按下了键\n");
      }
  }
  ```
  ```c
  #include <stdio.h>
  #include <conio.h>

  int main()
  {
      char input;
      if(kbhit()){
          //scanf("%c",&input);    
          input=getch();           //不需要按下回车键来读取
          printf("按下了键\n");
      }
  }
  ```
  <a name="8"></a>
+ **产生随机数的函数**
  ```c
  #include<stdlib.h>
  rand();
  ```
  <a name="9"></a>
+ **光标移动到原点位置进行重画(实现类似于清屏函数的效果)**
  ```c
  #include <windows.h>
  
  void gotoxy(int x,int y)//类似于清屏函数，光标移动到原点位置进行重画
  {
      HANDLE handle = GetStdHandle(STD_OUTPUT_HANDLE);
      COORD pos;
      pos.X = x;
      pos.Y = y;
      SetConsoleCursorPosition(handle,pos);
  }
  
  int main()
  {
      gotoxy(0,0);
  }
  ```
  <a name="10"></a>
+ **隐藏光标显示函数**
  ```c
  #include <windows.h>
  
  void HideCursor()
  {
      CONSOLE_CURSOR_INFO cursor_info={1,0};   //第二个值为0表示隐藏光标
      SetConsoleCursorInfo(GetStdHandle(STD_OUTPUT_HANDLE),&cursor_info);
  }
  
  int main()
  {
      HideCursor();
  }
  ```
  <br><br><br>
  [返回目录](#目录)
  <a name="11"></a>
+ **修改窗口大小(静态)**
  ```c
  #include <windows.h>
  system("mode con cols=30 lines=20");  //其中30为宽的值，20为高的值
  ```
  <a name="12"></a>
+ **修改窗口大小(动态)**
  ```c
  #include<stdio.h>
  #include<windows.h>

  void setWinSize(int height,int width)
  {
      char str[20];
      sprintf(str, "mode con: cols=%d lines=%d", height, width);
      system(str);
  }

  int main()
  {
      int height, width;
      scanf("%d %d", &height, &width);       //输入高和宽的值
      setWinSize(height,width);
  }
  ```
  <a name="13"></a>
+ **固定窗口大小**
  ```c
  #include <windows.h>
  void fixWinSize()  
  {
      HWND hWnd = GetConsoleWindow(); //获得cmd窗口句柄
      RECT rc;
      GetWindowRect(hWnd, &rc); //获得cmd窗口对应矩形

      //改变cmd窗口风格
      SetWindowLongPtr(hWnd,GWL_STYLE, GetWindowLong(hWnd, GWL_STYLE) & ~WS_THICKFRAME & ~WS_MAXIMIZEBOX & ~WS_MINIMIZEBOX);
  }
  
  fixWinSize();
  ```
  <a name="14"></a>
+ **修改窗体风格**
  ```c
  #include <windows.h>
  
  void setWinLong()
  {
      HWND hwnd = GetConsoleWindow();
      LONG Style;	//窗口风格
      Style = GetWindowLong(hwnd, GWL_STYLE);	 // 得到窗口风格
      Style = Style & ~WS_CAPTION;			 //去掉标题栏，网上可查选
      SetWindowLong(hwnd, GWL_STYLE, Style);	 //为窗口设置新的风格
  }
  ```
  <a name="15"></a>
+ **设置指定窗口的显示状态**
  ```c
  #include <windows.h>

  ShowWindow(FindWindowA("ConsoleWindowClass",NULL),SW_HIDE);     //隐藏窗口
  ShowWindow(FindWindowA("ConsoleWindowClass",NULL),SW_SHOW);     //显示窗口
  ```
  <a name="16"></a>
+ **修改窗口标题**

  > ***方法一：***
  ```c
  #include <windows.h>
  SetConsoleTitleA("name");
  ```
  > ***方法二：***
  ```c
  #include <windows.h>
  system("title name");
  ```
  <a name="17"></a>
+ **弹出消息框**
  ```c
  #include <windows.h>

  MessageBoxA(0,"内容","标题",MB_OK|MB_SYSTEMMODAL);  //MB_OK表示有确认键，MB_SYSTEMMODAL表示在窗口置顶
  ```
  <a name="18"></a>
+ **修改字体颜色、背景颜色**

  > ***方法一：***
  ```c
  #include <windows.h>
  system("color 07");     //(07)为默认的黑底白字。其中0为背景色，7为前景色
  
  /*
  颜色属性由两个十六进制数字指定 
  -- 第一个为背景色，第二个则为前景色。
  每个数字可以为以下任何值之一:
  0 = 黑色 8 = 灰色
  1 = 蓝色 9 = 淡蓝色
  2 = 绿色 A = 淡绿色
  3 = 湖蓝色 B = 淡浅绿色
  4 = 红色 C = 淡红色
  5 = 紫色 D = 淡紫色
  6 = 黄色 E = 淡黄色
  7 = 白色 F = 亮白色
  */
  ```
  > ***方法二：***
  ```c
  #include <windows.h>
  
  void SetColor(unsigned short BackGroundColor,unsigned short ForeColor)
  {
      HANDLE hCon=GetStdHandle(STD_OUTPUT_HANDLE);
      SetConsoleTextAttribute(hCon,(ForeColor%16)|(BackGroundColor%16*16));
  }
  
  SetColor(0,7);   //(0,7)为默认的黑底白字。其中0为背景色，7为前景色
  ```
  > ***示例：***
  ```c
  #include <windows.h>
  #include <stdio.h>

  void SetColor(unsigned short BackGroundColor,unsigned short ForeColor)
  {
      HANDLE hCon=GetStdHandle(STD_OUTPUT_HANDLE);
      SetConsoleTextAttribute(hCon,(ForeColor%16)|(BackGroundColor%16*16));
  }

  int main()
  {
      system("color 70");
      printf("方法一\n");

      int i,j;
      while(scanf("%d %d",&i,&j))
      {
          SetColor(i,j);
          printf("方法二\n");
      }
  }
  ```
  ![color.png](https://i.loli.net/2018/11/18/5bf0d8d1cd1eb.png)
  <a name="19"></a>
+ **修改文本颜色**
  ```c  
  #include <windows.h>
  SetConsoleTextAttribute(GetStdHandle(STD_OUTPUT_HANDLE), 2);	//设置颜色
  ```
  <a name="21"></a>
+ **添加背景音乐**
  ```c
  #pragma comment(lib,"Winmm.lib")
  //仅在VC下支持，需要的自行百度
  ```
  <a name="22"></a>
+ **计数函数**

  > ***方法一：***
  ```c
  #include <stdio.h>
  #include <time.h>
  #include <windows.h>

  int main()
  {
      clock_t start,end;
      start = clock();

      Sleep(2000);

      end = clock();
      printf("time=%f\n",(double)(end-start)/CLK_TCK);
  }
  ```
  > ***方法二：***
  ```c
  #include <stdio.h>
  #include <windows.h>

  int main()
  {
      DWORD end,start;
      start= GetTickCount();

      Sleep(2000);

      end= GetTickCount();
      printf("time=%d\n",end-start);
  }
  ```
+ **修改字体大小**
  ```c
  //暂未
  ```
  <a name="20"></a>
+ **修改窗体icon图标**

  Dev-C++ 新建项目->`Ctrl+H`(项目属性)
  <a name="23"></a>
+ **修改窗体透明度**
  ```c
  #include <windows.h>

  void setWinTransparent()
  {
      HWND hwnd = GetConsoleWindow();
      int ExdStyle = (int)GetWindowLong(hwnd, GWL_EXSTYLE);
      //通过SetWindowLong设置窗口的属性，多增加了一个WS_EX_LAYERED支持透明
      SetWindowLong(hwnd, GWL_EXSTYLE, ExdStyle | WS_EX_LAYERED);
      SetLayeredWindowAttributes(GetConsoleWindow(),RGB(255, 255, 255), 200, LWA_ALPHA);//200为透明度值（0-255）
  }

  int main()
  {
      setWinTransparent();
  }
  ```
+ **键盘输入上下左右，回车确定，Esc退出**
  ```c
  char input;
  while(1)
  {
      input=getch();
      if(input==27){            //Esc键ASCII码为27
      }
      if(input==13){            //回车键ASCII码为13
      }
      if(input!=-32) continue;  //避免因从键盘上输入的其他无关值影响程序进行
      input=getch();            //在读取上下左右ASCII码前必须添加
      if(input==72){            //上的ASCII码为72
      }
      if(input==80){            //下的ASCII码为80
      }
      if(input==75){            //左的ASCII码为75
      }
      if(input==77){            //右的ASCII码为77
      }
  }
  ```
  <br><br><br>
  [返回目录](#目录)
  
