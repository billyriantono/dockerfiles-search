# Version: 0.0.1
FROM ubuntu:latest

MAINTAINER Jessevan Zhang "jessevan.zhang@hotmail.com"

RUN echo "deb http://mirrors.163.com/ubuntu/ trusty-security main restricted universe multiverse\n" > /etc/apt/sources.list
RUN echo "deb http://mirrors.163.com/ubuntu/ trusty-updates main restricted universe multiverse\n" >> /etc/apt/sources.list
RUN echo "deb http://mirrors.163.com/ubuntu/ trusty-proposed main restricted universe multiverse\n" >> /etc/apt/sources.list
RUN echo "deb http://mirrors.163.com/ubuntu/ trusty-backports main restricted universe multiverse\n" >> /etc/apt/sources.list
RUN echo "deb-src http://mirrors.163.com/ubuntu/ trusty main restricted universe multiverse\n" >> /etc/apt/sources.list
RUN echo "deb-src http://mirrors.163.com/ubuntu/ trusty-security main restricted universe multiverse\n" >> /etc/apt/sources.list
RUN echo "deb-src http://mirrors.163.com/ubuntu/ trusty-updates main restricted universe multiverse\n" >> /etc/apt/sources.list
RUN echo "deb-src http://mirrors.163.com/ubuntu/ trusty-proposed main restricted universe multiverse\n" >> /etc/apt/sources.list
RUN echo "deb-src http://mirrors.163.com/ubuntu/ trusty-backports main restricted universe multiverse\n" >> /etc/apt/sources.list

RUN apt-get update --fix-missing


RUN apt-get -y install nginx --assume-yes 


#设置环境变量，永久有效
ENV TARGET_DIR /usr/local	

#设置工作目录
WORKDIR $TARGET_DIR


#ENTRYPOINT ["/usr/sbin/nginx"]

#CMD ["-h"]

ENTRYPOINT ["/bin/bash"]


WORKDIR /


EXPOSE 80

#指定运行容器的用户
#USER  myUser:myGroup

#添加卷
VOLUME ["/shared"]

#构建环境下的目录，文件添加到镜像中（ADD指令后的缓存无效）
COPY ./nginx.conf /data/conf/nginx/nginx.conf

ADD ./nginx.conf /bak/conf/nginx/nginx.conf

#ONBUILD: 构建触发器指令
ONBUILD ADD ./nginx.conf /onbuild/conf/nginx/nginx.conf

