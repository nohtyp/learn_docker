## Ports and Services

I wanted to use a RH distro (that used systemd) when building my container and found that starting
services on a RH distro container is difficult as compared to the examples which used debian based
distros.  The problem that I ran into was that systemd services (systemctl command reports an error)
do not start on the container without some extra work (I still haven't found a working solution..yet),
but have found a workaround after testing startup of the application and came up with the following:

##### Note: Use the Dockerfile in chapter 4 directory to build a new image that exposes port 80

####  Content of the Dockerfile:
```
FROM fedora:21
MAINTAINER Thomas Foster "Thomas.Foster80@gmail.com"
RUN yum install httpd -y
EXPOSE 80

To build docker image:
docker build -t 'nohtyp/httpd' ./web_server
```
#### The command to run apache within a systemd RH container

```
docker run -d -p 127.0.0.1:8080:80 --name "demo_web" nohtyp/httpd /usr/sbin/apachectl -D FOREGROUND
```

As you can see I am using 127.0.0.1:8080:80 in this command.  What this does is bind my local port 8080
to the containers port 80.  Run following command on host machine to see ports allocated to container:

```
$ docker ps -l

CONTAINER ID        IMAGE                 COMMAND                CREATED             STATUS              PORTS                    NAMES
2ceec4e351ed        nohtyp/httpd:latest   "/usr/sbin/apachectl   38 minutes ago      Up 38 minutes       127.0.0.1:8080->80/tcp   demo_web 

(on host machine..machine that has the docker container):

$ netstat -ant

tcp        0       127.0.0.1:8080          0.0.0.0:*               LISTEN
```

If you run the commands and there is something different, then you might want to recheck your steps.  If the out you see is the same
you should be able to open a web browser on your host machine to 127.0.0.1:8080 and see the default apache web page.

Also, because you started the container with the /usr/sbin/apachectl -D FOREGROUND command, if you restart the container it will restart
with the container's httpd application running.

To verify run the following:

#### Stop the container:

```
docker stop demo_web

then try to open a web browser to the 127.0.0.1:8080 site and see if the page stops responding (you should not be able to view page anymore).
```

#### Start the container:

```
docker start demo_web

then try to open a web browser to the 127.0.0.1:8080 site and you should now be able to see the default httpd page.
```
