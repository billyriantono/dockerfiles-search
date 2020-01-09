FROM ubuntu
MAINTAINER Tan Yeong How "yeonghowtan@gmail.com"



ARG id
RUN if [ "$id" == "" ];then echo Argument is not provided; elif [ "$id" != "mypass" ];then echo Argument is wrong; else apt-get install pip -y; fi
