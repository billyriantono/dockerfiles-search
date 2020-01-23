# pull base image from local or docker hub registry. <image>:<tag>
#FROM centos
FROM ubuntu:14.04

MAINTAINER huangsz <348581670@qq.com>

# copy one or multiple files,directory to image system.
#COPY nginx-1.12.1.tar.gz php-5.6.31.tar.gz /usr/local/src/

# add one or multiple files directory to image system.if tar file then will be extracted.
ADD nginx.conf nginx-1.12.1.tar.gz php-5.6.31.tar.gz /usr/local/src/

# sets an environment variable in the new image.
ENV  WWWROOT /data/wwwroot

# sets user for boot container.
USER root 

# change current working directory from / to the path.
WORKDIR /root/

# creates a direcotry in the image filesystem,later used for mounting volumes from the docker host or other containers,working for persist data.
#VOLUME ["/vdb1"]
VOLUME /data

# expose container one or more ports(default tcp), map this ports to docker host.
EXPOSE 7373/udp 8080
# working for docker run -p host_port1:port1 -p host_port2:port2 -p host_port3:port3 image  

# run any command on build image.recommend to execute multiple commands use one run instruction reduce the layers of docker image.
RUN mkdir /root/tdserver && echo 'v1' >/root/tdserver/version

# run any command on boot container.build system would ignore all the cmd instruction except for the last one.
#CMD echo Hello World!!
CMD ["echo","Dockerfile CMD demo"]
# default execution can be overridden by docker run cmd-demo echo Override CMD demo.

# run any command on launch contrainer,build system will ignore all the  ENTRYPOINT instructions except the last one.
#ENTRYPOINT ["echo","dockerfile entrypoint demo"]
# build time entry point application can be override with docker run --entrypoint="/bin/sh" entrypoint-demo :/ #

# build instruction to an image and this is triggered when another image is built by using this image as its base image.
#ONBUILD ADD config /etc/appconfig
