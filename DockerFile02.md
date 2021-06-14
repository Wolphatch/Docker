1. 步骤
    1.1 dockerfile 编写
    1.2 docker buile 创建镜像
    1.3 docker run 运行
    1.4 docker push 发布

2. Tag
    
    ```FROM <image>:<tag>```
    
    ```RUN ["executable", "param1", "param2"]```
    
    ```COPY ["<源路径1>",... "<目标路径>"]```
  
    ```ADD ["<源路径>",... "<目标路径>"]```
  
    ```ENV <key1>=<value1> <key2>=<value2>...```
  
    ```EXPOSE <port> [<port>...]```
  
    ```VOLUME ["/data"]```
  
    ```ENTRYPOINT ["executable", "param1", "param2"]```
  
    ```ARG <name>[=<default value>]```
  
    http://www.ityouknow.com/docker/2018/03/15/docker-dockerfile-command-introduction.html
   
