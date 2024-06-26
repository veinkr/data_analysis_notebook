
列出所有容器ID

```bash
docker ps -aq
```

查看所有运行或者不运行容器

```bash
docker ps -a
```

停止所有的container（容器），这样才能够删除其中的images：

```bash
docker stop $(docker ps -a -q) 或者 docker stop $(docker ps -aq)
```

如果想要删除所有container（容器）的话再加一个指令：

```bash
docker rm $(docker ps -a -q) 或者 docker rm $(docker ps -aq)
```

查看当前有些什么images

```bash
docker images
```

删除images（镜像），通过image的id来指定删除谁

```bash
docker rmi <image id>
```

想要删除untagged images，也就是那些id为的image的话可以用

```bash
docker rmi $(docker images | grep "^<none>" | awk "{print $3}")
```

要删除全部image（镜像）的话

```bash
docker rmi $(docker images -q)
```

强制删除全部image的话

```bash
docker rmi -f $(docker images -q)
```

从容器到宿主机复制

```bash
docker cp tomcat：/webapps/js/text.js /home/admin
docker  cp 容器名:  容器路径       宿主机路径
```

从宿主机到容器复制

```bash
docker cp /home/admin/text.js tomcat：/webapps/js
docker cp 宿主路径中文件      容器名  容器路径   2
```

删除所有停止的容器

```bash
docker container prune
```

删除所有不使用的镜像

```bash
docker image prune --force --all或者docker image prune -f -a
```

停止、启动、杀死、重启一个容器

```bash
docker stop Name或者ID
docker start Name或者ID
docker kill Name或者ID
docker restart name或者ID
```

docker进入容器，查看配置文件

```bash
docker exec ：在运行的容器中执行命令
    -d :分离模式: 在后台运行
    -i :即使没有附加也保持STDIN（标准输入） 打开,以交互模式运行容器，通常与 -t 同时使用；
    -t: 为容器重新分配一个伪输入终端，通常与 -i 同时使用；
docker exec -it  f94d2c317477 /bin/bash
```

出现root@f94d2c317477:/usr/share/elasticsearch/config\# vi elasticsearch.yml

bash: vi: command not found

```bash
apt-get update && apt-get install vim -y
```

修改配置、退出容器

```bash
1、如果要正常退出不关闭容器，请按Ctrl+P+Q进行退出容器
2、如果使用exit退出，那么在退出之后会关闭容器，可以使用下面的流程进行恢复
使用docker restart命令重启容器
使用docker attach命令进入容器
```

