# DockerNote

加速器 http://guide.daocloud.io/dcs/daocloud-9153151.html#docker-toolbox
<h3>按格式输出所有image</h3>
docker image ls --format "table {{.ID}}\t{{.Repository}}\t{{.Tag}}"  列出所有镜像
* 效果
<table>
  <tr>
      <td>IMAGE ID</td><td>REPOSITORY </td><td>TAG</td>
  </tr>
    <tr>
      <td>45sd15151asd</td><td>redis</td><td>latest</td>
  </tr>
</table>

<h3>删除指定image</h3>
我们可以用镜像的完整 ID，也称为  长 ID  ，来删除镜像。使用脚本的时候可能会用长 ID，但
是人工输入就太累了，所以更多的时候是用  短 ID  来删除镜像。 docker image ls  默认列出
的就已经是短 ID 了，一般取前3个字符以上，只要足够区分于别的镜像就可以了。
比如这里，如果我们要删除  redis:alpine  镜像，可以执行：
$ docker image rm 45

我们需要删除所有仓库名为  redis  的镜像：
$ docker image rm $(docker image ls -q redis)
或者删除所有在  mongo:3.2  之前的镜像：
$ docker image rm $(docker image ls -q -f before=mongo:3.2)

<h3>快速部署rabbitmq</h3>

docker pull rabbitmq:management
创建并运行容器：

复制代码
docker run -d --hostname my-rabbit --name rabbit -p 8080:15672 rabbitmq:management
--hostname：指定容器主机名称
--name:指定容器名称
-p:将mq端口号映射到本地

或在运行时设置用户和密码
docker run -d --hostname my-rabbit --name rabbit -e RABBITMQ_DEFAULT_USER=admin -e RABBITMQ_DEFAULT_PASS=admin -p 15672:15672 -p 5672:5672 -p 25672:25672 -p 61613:61613 -p 1883:1883 rabbitmq:management

 15672：控制台端口号

 5672：应用访问端口号
