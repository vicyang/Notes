* 预备  
  [lua](http://www.lua.org/download.html)  
  [srlua](https://github.com/LuaDist/srlua)  
  [nuwen MinGW](https://nuwen.net/mingw.html)  
  [cmake](https://cmake.org/download/)  
  设置好环境变量，确保能够随时调用 gcc, make, windres, cmake  
  
* ### Step1  
  下载源码包 [lua-5.3.4.tar.gz](http://www.lua.org/ftp/lua-5.3.4.tar.gz)，以及 [srlua](https://github.com/LuaDist/srlua)  
  分别解压，这里假设 lua 源码位于 D:\Lib\lua-5.3.4  
  srlua 源码位于 D:\Lib\srlua-master  
  
* ### Step2 方案A  
  进入 D:\Lib\lua-5.3.4\src 执行 make （如果出错了请自己找方法解决）  
  进入 D:\Lib\srlua-master 设置环境变量，  
  > set PATH=D:\Lib\lua-5.3.4\src;%PATH%  
  > cmake -G "MinGW Makefiles" .  
  > make  
  
  Notes: 一开始执行 cmake 是失败的，打开 cmake 目录发现 FindLua.cmake 猜想应该把 lua 源码以及运行环境添加到 %PATH%，然后才成功  
  
* ### Step2 方案B  
  不使用 CMake，只用 MinGW GCC  
  将以下内容保存到 compile_srlua.bat  
  ```bat
  @echo off
  
  if not exist bin mkdir bin
  
  set "INC=-ID:\Lib\lua-5.3.4\src"
  set "LIB=-LD:\Lib\lua-5.3.4\src"
  
  windres glue.rc glue_logo.o
  gcc -o ./bin/glue.exe glue.c glue_logo.o
  
  windres srlua.rc srlua_logo.o
  gcc -o  ./bin/srlua.exe %INC% %LIB% wmain.c srlua.c srlua_logo.o -llua -lm
  gcc -o ./bin/wsrlua.exe %INC% %LIB% wmain.c srlua.c srlua_logo.o -llua -lm -mwindows
  
  pause
  ```
      
  Notes:  
  1. windres和图标生成有关，参考自：[让你用GCC编译的程序拥有一个自定义的.ico图标 ](http://blog.csdn.net/mzlogin/article/details/6647460)  
  2. -llua -lm 参考自 srlua-master/Makefile  
  原先的 Makefile 编译参数中含有 -ldl，编译提示 `cannot find -ldl`，似乎是 linux 下的库，去掉后编译通过。  
  3. 编译 wsrlua 时，加 -mwindows 参数以使程序运行时不显示终端。  
  
  
