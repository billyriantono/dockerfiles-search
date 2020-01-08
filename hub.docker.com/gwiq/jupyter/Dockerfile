FROM jupyter/all-spark-notebook
MAINTAINER Jakub Liska <liska.jakub@gmail.com>

RUN apt-get update -y
RUN apt-get install wget -y
RUN wget -O - http://download.gluster.org/pub/gluster/glusterfs/3.6/LATEST/Debian/jessie/pub.key | apt-key add -
RUN echo deb http://download.gluster.org/pub/gluster/glusterfs/3.6/LATEST/Debian/jessie/apt jessie main > /etc/apt/sources.list.d/gluster.list
RUN apt-get update -y
RUN apt-get install python python-pip curl inotify-tools glusterfs-client -y
RUN apt-get clean

RUN pip install --upgrade awscli

RUN mkdir /root/work && mkdir /root/.jupyter && mkdir /root/.jupyter/custom
WORKDIR /root/work

COPY jupyter_notebook_config.py /root/.jupyter/
COPY custom.css /root/.jupyter/custom/

COPY start-notebook.sh /usr/local/bin/
