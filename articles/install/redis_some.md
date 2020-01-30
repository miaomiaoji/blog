
## redis安装
redis虽然有windows相关版本，但是更新并不及时版本也不多。于是在windows上使用WSL来使用redis。
## 安装wsl
- windows安装wsl
  - 控制面板——程序——启用或关闭windows功能——适用于Linux的Windows子系统——重启
  - 打开Microsoft store，搜索wsl，选择一个安装，比如ubuntu
  - 安装成功之后，设置一个用户名和密码
- 在选择的文件夹下，windows系统右键即可打开linux shell
## 使用ubuntu安装redis
- 使用wsl安装redis——参考[Running Redis on Windows 10](https://redislabs.com/blog/redis-on-windows-10/)
  - 安装
    ```
    > sudo apt-get update
    > sudo apt-get upgrade
    > sudo apt-get install redis-server
    > redis-cli -v
    ```
  - 重启redis 服务器
    ```
    >  sudo service redis-server restart
    ```
  - 运行redis-cli，并测试
    ```
    $ redis-cli 
    127.0.0.1:6379> set user:1 "Jane"
    127.0.0.1:6379> get user:1
    "Jane"
    ``` 
  - 关闭服务器
    ```
    > sudo service redis-server stop
    ```
  - 卸载redis-server
        ```
        sudo apt-get remove --purge redis-server
        sudo apt-get autoremove --purge redis-server
        ```
## 下载安装包以及安装redis-server
```
$ sudo apt-get update
$ sudo apt-get install make
$ sudo apt-get install gcc

<!-- 切换你想要安装的文件夹  -->
wget http://download.redis.io/redis-stable.tar.gz
tar xvzf redis-stable.tar.gz
cd redis-stable
make
```
参考地址——<https://redis.io/topics/quickstart>

## 总结
使用ubuntu安装速度比较快，不需要手动配置就可以随时输入`sudo service redis-server restart`打开服务器。

自己下载安装速度较慢，可以每次切换到redis目录下启动redis服务器，或者复制redis-server和redis-cli到usr/local/bin
```
sudo cp src/redis-server /usr/local/bin/
sudo cp src/redis-cli /usr/local/bin/
```