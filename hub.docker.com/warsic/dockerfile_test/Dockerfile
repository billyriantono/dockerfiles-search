FROM centos:latest

LABEL maintainer="Warsic Dia warsicdia@gmail.com"

# install package and monitoring tools
RUN     yum -y update && \
        yum -y install epel-release && \
        yum -y install wget unzip git htop iotop iftop && \
        yum -y install git 
