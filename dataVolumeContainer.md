1. 如何容器间数据同步

     ```docker run -it --name U1 -v /data ubuntu:18.04```创建数据卷容器 U1, 数据卷位置为/data

    ```docker run --name U2 --volumes-from U1 -it ubuntu:18.04```创建数据卷容器U2, 同步U1数据卷的数据
    
    ```docker run --name U3 --volumes-from U1 -it ubuntu:18.04```创建数据卷容器U3, 同步U1数据卷的数据
    
    每当U1的/data目录发生改变,U2, U3的/data目录都会改变
    
2.  ```docker volume ls```
3.  ```docker volume prune``` 删除所有未使用的卷
4.  一旦数据持久化到了主机,就不会被删除,否则最后一个使用卷的容器被删除后,卷的数据就没了.
