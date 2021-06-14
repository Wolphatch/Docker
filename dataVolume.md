1. 怎么持久化容器中的数据？

    把数据储存在本地，需要容器之间需要求一个数据共享技术。
    docker 容器中产生的数据同步到本地
    手段是将容器内的目录挂载到本地
    
2. 使用 -v 命令挂载
    ```docker run -it -v [host path]:[container path] -p 8080:8080 [image]```
    
    ```docker run -it -v ~/home/dockerUbuntuHome:/home -p 8080:8080 ubuntu:18.04```
    
    每次在容器的/home下做修改，主机的~/home/dockerUbuntuHome会同步修改，这种绑定是双向的

3.用处是：可以在host上直接修改容器们的配置文件而不用进入容器

    3.1 example：
    
         ```docker pull mysql:latest```
         
         挂载两个目录，使用-e 设置配置项
         ```docker run -d -p 3310:3306 -v /home/mysql/conf:/etc/mysql/conf.d -v /home/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123 mysql:tag```
         
         
         ```-v```:挂载文件
         
         ```-d```：后台运行
         
         ```-it```：前台运行
         
         ```-e```：环境配置
         
         ```--name```：容器名字
         
         ```-p```：默认端口映射
         
    3.2 ```docker volume ls``` 查看所有卷的情况
    
    3.3 ```docker volume inspect [Container]```
    
    3.4 ```-v```后面加上:ro 或者:rw可以更改权限, 一旦设定权限，就无法改变。
    
        ```docker run -d -p 3310:3306 -v /home/mysql/conf:/etc/mysql/conf.d -v /home/mysql/data:/var/lib/mysql:rw -e MYSQL_ROOT_PASSWORD=123 mysql:tag```
        如果使用ro，容器内部就无法对此目录进行写的操作（只读）。 
