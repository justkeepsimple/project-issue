
一、选定安装文件目录　yum install -y gcc gcc-c++

二、安装PCRE库

    wget ftp://ftp.csx.cam.ac.uk/pub/software/programming/pcre/pcre-8.39.tar.gz 
    tar -zxvf pcre-8.37.tar.gz
    cd pcre-8.34
    ./configure
    make
    make install
    
三、安装zlib库

    wget http://zlib.net/zlib-1.2.11.tar.gz
    tar -zxvf zlib-1.2.11.tar.gz
    cd zlib-1.2.11
    ./configure
    make
    make install
    
 
 四、安装openssl
 ./configure  --prefix=/zgg/nginx/usr/local/ 指定安装路径
 
 五、安装nginx
 
    wget http://nginx.org/download/nginx-1.1.10.tar.gz
    tar -zxvf nginx-1.1.10.tar.gz
    cd nginx-1.1.10
    ./configure
    make
    make install
    
    
六、nginx重启、关闭、启动
   
     启动代码格式：nginx安装目录地址 -c nginx配置文件地址
     
     
     1、验证nginx配置文件是否正确

    方法一：进入nginx安装目录sbin下，输入命令./nginx -t

    看到如下显示nginx.conf syntax is ok

    nginx.conf test is successful

    说明配置文件正确！
    
    
    在启动命令-c前加-t
    
    
    2、重启Nginx服务

    方法一：进入nginx可执行目录sbin下，输入命令./nginx -s reload 即可
    
    方法二：查找当前nginx进程号，然后输入命令：kill -HUP 进程号 实现重启nginx服务
