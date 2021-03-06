1. Start:  
  
	```systemctl start docker```

2. Test whether successfully started:
   
  	```docker version```
   
3. Run
  
  	```docker run [image]```
  
4. Every container looks like a small linux VM. 
  
  	Containers are isolated.
  	Each of them has ports.
  
5. Why docker is faster than VM?
	
	Every VM instance is a complete Linux system (os). 
	Docker uses the os of the current machine directly. It doesn't need to load a new os.
	
6. Baisc image command:
	
	6.1 ```docker --help```
	
	6.2 ```docker info```
	
		Have a look at the info of the docker
	
	6.3 ```docker images```
	
		Check all local images
		
		```docker images -a```: 查看所有images
		```docker images -q```: 只查看镜像ID
		
	6.4 ```docker search```
	
		```docker search mysql```: 搜索images
			
		```docker search mysql -f STARS=5000```：过滤
		
	6.5 docker pull
	
		```docker pull mysql:5.7.34```
	
		```docker pull``` 使用分层更新，新版本images中，旧版本已存在的文件不会下载
		
	6.6 ```docker rmi -f [IMAGE ID]``` 删除image
	
		```docker rmi -f $(docker images -aq)```: 查找所有的IMAGE ID 并删除

7. Container command:
	
	7.1 ```docker run [param] image```
	
	7.2 ```docker run --name="ubuntu01" image``` 给容器一个名字
	
	7.3 ```docker run -d image```  后台运行
	
	7.4 ```docker run -it ubuntu /bin/bash``` 使用交互方式运行，进入容器查看内容
		
		7.4.1 如果启动了一个ubuntu，会从 ```root@主机名``` 变为 ```root@镜像ID```
	
	7.5 ```docker run -p 8080:8080 image``` 指定端口
	
		7.5.1 -p 主机端口:容器端口
	
	7.6 ```docker run -P image``` 随机指定端口
	
	7.7 ```docker ps```: List all running Contained
		
		7.7.1 ```docker ps -a```: 包括历史运行的容器
		
		7.7.2 ```docker ps -n=1```: 显示最近一个运行的容器
		
		7.7.3 ```docker ps -q```: 显示容器的编号
		
	7.8 ```Ctrl + P + Q```:容器不停止但退出
	
	7.9 ```docker rm [Container ID]```:删除容器
	
		```docker rm $(docker ps -aq)```: 删除所有容器
	
	7.10 ```docker start [Container ID]```
	
	7.11 ```docker restart [Container ID]```
	
	7.12 ```docker stop [Container ID]```
	
	7.13 ```docker kill [Container ID]```

8. Other commands

	8.1 ```docker run -d ubuntu```
		
		if 容器在后台运行，就必须要有一个前台进程。 如果docker发现没有应用，就会自动停止
		
	8.2 ```docker logs -f -t --tail 10 [Container ID]``` 显示容器的倒数10行日志，带时间戳
	
	8.3 ```docker top [Container ID]``` 查看进程信息
		
	8.4 ```docker inspect [Container ID]``` 查看容器信息	
		
9. Commands in Containers

	9.1 ```docker exec -it [Container ID] /bin/bash``` 以交互模式进入容器，开启一个新的command line
	
	9.2 ```docker attach [Container ID]``` 进入容器正在执行的终端
	
	9.3 ```docker cp [Container ID]:[PATH in the Container] [Host Path]```从容器拷贝文件到主机
	
	9.4 ```docker cp [Host Path] [Container ID]:[PATH in the Container]```从主机拷贝文件到容器
		
  
  
