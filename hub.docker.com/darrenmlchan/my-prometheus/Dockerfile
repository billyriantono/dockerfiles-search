FROM ubuntu:latest

##USER GROUP TO BE ADDED

#REFERENCE:
#https://www.rosehosting.com/blog/ubuntu-crontab/
#https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-using-the-repository
#https://askubuntu.com/questions/509852/why-does-apt-get-abort-by-itself-as-though-id-pressed-n

RUN apt-get update && apt-get upgrade; \
    apt-get install cron

#"-y" indicates to confirm to install specified component.    
RUN apt-get -y install \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common

RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - 

RUN add-apt-repository \
"deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" 

RUN apt-get update

RUN apt-get -y install docker-ce

RUN apt-get -y install sudo

RUN apt-get -y install busybox-static

#RUN apt-get -y install cron
RUN apt-get -y install vim-tiny
#RUN apt-get -y install nano




