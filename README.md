# 一、用处
> 避免每次都重装php开发环境，保持环境的一致

前置需求，自己完成

- docker
- docker-compose：多个容器管理工具

# 二、快速使用

1. 在env文件下，配置代码工作目录，CODE_PATH
2. 配置nginx服务，容器里的目录为/var/www，文件映射到了CODE_PATH
3. 启动所有服务：docker-compose up -d
    首次启动需要编译，时间会长，第二次秒开

# 三、默认配置

版本：

1. nginx：1.19.1
2. mysql：5.7.31
3. redis：5.0.9
4. memcached：1.6.6
5. php5：5.6.40
6. php7：7.4.9

配置文件：当前目录下服务下配置目录中，自己可以定义


# 四、启动，关闭

1. 停止所有 ：docker-compose stop
2. 启动所有 ：docker-compose start
3. 单个启动 ：docker-compose start nginx
4. 单个停止 ：docker-compose stop nginx

# 。。

大部分情况下，用了mysql的服务，创建省事
