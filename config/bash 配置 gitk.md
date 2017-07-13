### bash 配置 gitk

1. 下载sudo apt-get install gitk 

2. 配置环境变量 export DISPLAY=:0.0

   bash下配置方法如下：

    1.  全部用户组配置  vim /etc/profile  添加 export DISPLAY=:0.0

    2.  配置当前用户 比如我的用户cxpro 。vim .bashrc 添加export DISPLAY=:0.0

        ​

3. 下载[Xming X ](https://sourceforge.net/projects/xming)

4. 最后启动Xming X  ,输入gitk 即可运行。