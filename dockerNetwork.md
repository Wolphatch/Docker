1. ```docker exec -it 2b80856e6877 cat /etc/hosts```

```

fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
172.17.0.2      2b80856e6877

```
2. 容器互通

 
   创建容器
   ```docker run -p 8081:8081 --network flink-network --name m1 mysql:latest```启动容器1

    ```docker run -p 8081:8081 --network flink-network --name m2 mysql:latest```启动容器2

    进入容器分别在两个容器中安装ifconfig和ping

    ```apt-get update```

    ```apt-get upgrade```

    ```apt-get install iputils-ping```

    ```apt-get install net-tools```

    使用ifconfig查看互相IP地址,并通信

    ```ifconfig```

    ```ping [IP of another container]```


3
  
