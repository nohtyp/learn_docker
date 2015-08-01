## First docker container

1. Create directory `web_server`.
2. Create file named 'Dockerfile'.
3. Add the following instructions to the 'Dockerfile'.

#### Note: All options must be capital.
   
   1. FROM -> This describes the particuhelar version of os you are going to use to       
      install your application. Example: FROM fedora:21 or docker pull fedora (this would pull down the latest image).
   2. MAINTAINER -> This describes who maintains the current image.  This will have the maintainers name and email address.
      Example: MAINTAINER  Thomas Foster "Thomas.Foster80@gmail.com"
   3. RUN -> These are the commands that you will run in the container while it's building.
      Example: RUN yum install httpd

## Build contai ner using docker build

1. To build the container run the following command (while in chapter2 directory): docker build ./web_server

Output:
```
docker build ./web_server/
Sending build context to Docker daemon 2.048 kB
Sending build context to Docker daemon 
Step 0 : FROM fedora:21
21: Pulling from docker.io/fedora
e26efd418c48: Already exists 
48ecf305d2cf: Already exists 
docker.io/fedora:21: The image you are pulling has been verified. Important: image verification is a tech preview feature and should not be relied on to provide security.
Digest: sha256:629041de92f616272337ef1bc2e3a18c9c04a8de68eae74eb04ddf4907e797b6
Status: Downloaded newer image for docker.io/fedora:21
 ---> e26efd418c48
Step 1 : MAINTAINER Thomas Foster "Thomas.Foster80@gmail.com"
 ---> Running in a70f06f707c6
 ---> 8a6188609bfe
Removing intermediate container a70f06f707c6
Step 2 : RUN yum install httpd -y
 ---> Running in 3470f06047b1
Resolving Dependencies
--> Running transaction check
---> Package httpd.x86_64 0:2.4.16-1.fc21 will be installed
--> Processing Dependency: httpd-tools = 2.4.16-1.fc21 for package: httpd-2.4.16-1.fc21.x86_64
--> Processing Dependency: httpd-filesystem = 2.4.16-1.fc21 for package: httpd-2.4.16-1.fc21.x86_64
--> Processing Dependency: system-logos-httpd for package: httpd-2.4.16-1.fc21.x86_64
--> Processing Dependency: httpd-filesystem for package: httpd-2.4.16-1.fc21.x86_64
--> Processing Dependency: /etc/mime.types for package: httpd-2.4.16-1.fc21.x86_64
--> Processing Dependency: libaprutil-1.so.0()(64bit) for package: httpd-2.4.16-1.fc21.x86_64
--> Processing Dependency: libapr-1.so.0()(64bit) for package: httpd-2.4.16-1.fc21.x86_64
--> Running transaction check
---> Package apr.x86_64 0:1.5.1-3.fc21 will be installed
---> Package apr-util.x86_64 0:1.5.4-1.fc21 will be installed
---> Package fedora-logos-httpd.noarch 0:21.0.5-1.fc21 will be installed
---> Package httpd-filesystem.noarch 0:2.4.16-1.fc21 will be installed
---> Package httpd-tools.x86_64 0:2.4.16-1.fc21 will be installed
---> Package mailcap.noarch 0:2.1.43-1.fc21 will be installed
--> Finished Dependency Resolution

Dependencies Resolved

================================================================================
 Package                  Arch         Version              Repository     Size
================================================================================
Installing:
 httpd                    x86_64       2.4.16-1.fc21        updates       1.2 M
Installing for dependencies:
 apr                      x86_64       1.5.1-3.fc21         fedora        111 k
 apr-util                 x86_64       1.5.4-1.fc21         fedora         96 k
 fedora-logos-httpd       noarch       21.0.5-1.fc21        fedora         33 k
 httpd-filesystem         noarch       2.4.16-1.fc21        updates        24 k
 httpd-tools              x86_64       2.4.16-1.fc21        updates        85 k
 mailcap                  noarch       2.1.43-1.fc21        fedora         36 k

Transaction Summary
================================================================================
Install  1 Package (+6 Dependent packages)

Total download size: 1.6 M
Installed size: 4.5 M
Downloading packages:
--------------------------------------------------------------------------------
Total                                              652 kB/s | 1.6 MB  00:02     
Running transaction check
Running transaction test
Transaction test succeeded
Running transaction
  Installing : apr-1.5.1-3.fc21.x86_64                                      1/7 
  Installing : apr-util-1.5.4-1.fc21.x86_64                                 2/7 
  Installing : httpd-tools-2.4.16-1.fc21.x86_64                             3/7 
  Installing : httpd-filesystem-2.4.16-1.fc21.noarch                        4/7 
  Installing : fedora-logos-httpd-21.0.5-1.fc21.noarch                      5/7 
  Installing : mailcap-2.1.43-1.fc21.noarch                                 6/7 
  Installing : httpd-2.4.16-1.fc21.x86_64                                   7/7 
  Verifying  : mailcap-2.1.43-1.fc21.noarch                                 1/7 
  Verifying  : httpd-tools-2.4.16-1.fc21.x86_64                             2/7 
  Verifying  : apr-1.5.1-3.fc21.x86_64                                      3/7 
  Verifying  : apr-util-1.5.4-1.fc21.x86_64                                 4/7 
  Verifying  : fedora-logos-httpd-21.0.5-1.fc21.noarch                      5/7 
  Verifying  : httpd-2.4.16-1.fc21.x86_64                                   6/7 
  Verifying  : httpd-filesystem-2.4.16-1.fc21.noarch                        7/7 

Installed:
  httpd.x86_64 0:2.4.16-1.fc21                                                  

Dependency Installed:
  apr.x86_64 0:1.5.1-3.fc21                                                     
  apr-util.x86_64 0:1.5.4-1.fc21                                                
  fedora-logos-httpd.noarch 0:21.0.5-1.fc21                                     
  httpd-filesystem.noarch 0:2.4.16-1.fc21                                       
  httpd-tools.x86_64 0:2.4.16-1.fc21                                            
  mailcap.noarch 0:2.1.43-1.fc21                                                

Complete!
 ---> 4f9997a3321c
Removing intermediate container 3470f06047b1
Successfully built 4f9997a3321c
```

The build command created a new	image which can be listed with the following command:
`docker images`

As you can see the image does not have a valid tag (which could also be the name). This is decided
when you build the container (see below).

#### Without tag
```
docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
<none>              <none>              4f9997a3321c        27 minutes ago      451.7 MB
```

#### Note: This was how I tagged the image: docker build -t "nohtyp/web_server:v1" ./web_server

### With tag
```
docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
nohtyp/web_server   v1                  4f9997a3321c        39 minutes ago      451.7 MB
```
