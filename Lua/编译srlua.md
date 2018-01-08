* 预备  
  [lua官网](http://www.lua.org/download.html)  
  [srlua](https://github.com/LuaDist/srlua)  
  [nuwen MinGW](https://nuwen.net/mingw.html)  
  [cmake](https://cmake.org/download/)  
  设置好环境变量，确保能够随时调用 gcc, make, windres, cmake  

* Step1  
  下载源码包 [lua-5.3.4.tar.gz](http://www.lua.org/ftp/lua-5.3.4.tar.gz)，以及 [srlua](https://github.com/LuaDist/srlua)  
  分别解压，这里假设 lua 源码位于 D:\Lib\lua-5.3.4  
  srlua 源码位于 D:\Lib\srlua-master  

* Step2  
  进入 D:\Lib\lua-5.3.4\src 执行 make （如果出错了请自己找方法解决）  
  进入 D:\Lib\srlua-master 设置环境变量，
  > set PATH=D:\Lib\lua-5.3.4\src;%PATH%  
  > cmake -G "MinGW Makefiles" .  
  > make  



