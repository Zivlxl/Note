#### 终端出现（base）

1.  背景
       由于最近需要在Linux中使用Python3，同时为了方便管理，故安装了anaconda3。

2. 现象
       为了快速安装，故安装过程中一直无脑enter，于是在安装完成后，发现在Linux终端用户名多了一个“(base)”字样，如下：

3.  解决

   1. 单次更改

      a、使用 conda deactivate 命令可去除base

      b、当然，如果你觉得这个base看着也挺舒服的，那可以使用conda activate base增加base

   2. 永久更改
          可以通过修改conda的配置来实现永久更改。
      step1：使用conda config --show查看conda的配置，如下：

      可以发现，之所以会出现base，是因为框中参数在作妖，即默认启动base，症状有了，接下来对症下药就行！！

      step2：使用 conda config --set auto_activate_base False 命令将其设置为False即可