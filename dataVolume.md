1. 怎么持久化容器中的数据？

    把数据储存在本地，需要容器之间需要求一个数据共享技术。
    docker 容器中产生的数据同步到本地
    手段是将容器内的目录挂载到本地
    
2. 使用 -v 命令挂载
    ```docker run -it -v [host path]:[container path] -p 8080:8080 [image]```
    
    ```docker run -it -v ~/home/dockerUbuntuHome:/home -p 8080:8080 ubuntu:18.04```
    
    每次在容器的/home下做修改，主机的~/home/dockerUbuntuHome会同步修改，这种绑定是双向的
    
    使用```docker inspect ID```可以看到mount的信息：
    ```
     "Mounts": [
            {
                "Type": "bind",
                "Source": "/home/zac/dockerProj/mysql",
                "Destination": "/home",
                "Mode": "",
                "RW": true,
                "Propagation": "rprivate"
            }
        ]
    ```
    
    
3. 用处是：可以在host上直接修改容器们的配置文件而不用进入容器

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
         
      一旦挂载，就算是本地没有的文件也会被创建。 容器就算被删掉，本地的数据也是在的。
         
    3.2 ```docker volume ls``` 查看所有卷的情况
    
    3.3 ```docker volume inspect [Container]```
    
    3.4 ```-v```后面加上:ro 或者:rw可以更改权限, 一旦设定权限，就无法改变。
    
        ```docker run -d -p 3310:3306 -v /home/mysql/conf:/etc/mysql/conf.d -v /home/mysql/data:/var/lib/mysql:rw -e MYSQL_ROOT_PASSWORD=123 mysql:tag```
        如果使用ro，容器内部就无法对此目录进行写的操作（只读）。 



4. 具名、匿名挂载
    
    4.1  匿名 ``` docker run -d -P --name nginx  -v /etc/nginx nginx:latest ```
    
        ```-d```: 后台运行
        
        ```-P```: 随机指定端口
        
        ```docker volume ls```: 显示所有的卷的挂载
        
        此处-v之后 没有指定宿主机地址，运行volume ls之后：
        
        DRIVER    VOLUME NAME
        local     486328e7428197309b1fcfa1ea556d0078e4b1c18059c9a48032c36a724a825b
        
    4.2 匿名挂载的盘可以用docker volume inspect去检查宿主机的mount点在哪里。 但是Windows上有个问题就是这个mointpoint不存在。。。（WSL2）    
    ```

    docker volume inspect  486328e7428197309b1fcfa1ea556d0078e4b1c18059c9a48032c36a724a825b
    [
        {
            "CreatedAt": "2021-08-18T01:20:58Z",
            "Driver": "local",
            "Labels": null,
            "Mountpoint": "/var/lib/docker/volumes/486328e7428197309b1fcfa1ea556d0078e4b1c18059c9a48032c36a724a825b/_data",
            "Name": "486328e7428197309b1fcfa1ea556d0078e4b1c18059c9a48032c36a724a825b",
            "Options": null,
            "Scope": "local"
        }
    ]

    ```
    
5. 使用dockerfile去做挂载
    5.1 Dockerfile

        ``` Dockerfile
        #以ubuntu 18.04 为基础
        FROM ubuntu:18.04

        #挂载目录，匿名挂载
        VOLUME ["volume1","volume2"]

        CMD echo "---endd---"

        CMD /bin/bash

        ```

    5.2 生成镜像
         
         ```docker build -f Dockerfile -t testubuntu:0.1 .```
    5.3 运行镜像
        ```docker run -it -P --name ubuntu01  ba4524b60163```
    5.4 查看容器的挂载卷
        ```docker inspect cf007cbad0ac```
        
6. 
    
        
        
        
        
