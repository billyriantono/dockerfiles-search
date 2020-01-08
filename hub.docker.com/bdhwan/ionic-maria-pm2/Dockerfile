FROM ubuntu:18.04
LABEL maintainer=”bdhwan@gmail.com”

USER root
RUN apt-get update
RUN apt-get install sudo
RUN apt-get install -y apt-utils
RUN apt-get install -y curl
RUN apt-get install -y git
RUN sudo apt-get install -y gnupg
RUN curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
RUN sudo apt-get install -y nodejs
RUN sudo npm install -g npm@6.9.0
RUN sudo npm install -g ionic@4.12.0
RUN sudo npm install -g cordova@9.0.0
RUN sudo npm install -g git-upload
RUN sudo npm install -g @angular/cli@7.3.9
RUN sudo npm install -g pm2
RUN sudo npm i -g cordova-res@0.3.0 --unsafe-perm

RUN cordova telemetry on
RUN sudo apt-get install -y software-properties-common 
RUN sudo apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xF1656F24C74CD1D8
RUN sudo add-apt-repository 'deb [arch=amd64] http://mirror.zol.co.zw/mariadb/repo/10.3/ubuntu bionic main'
RUN sudo apt update
RUN ["/bin/bash", "-c", "debconf-set-selections <<< 'mariadb-server-10.3 mysql-server/root_password password password'"]
RUN ["/bin/bash", "-c", "debconf-set-selections <<< 'mariadb-server-10.3 mysql-server/root_password_again password password'"]
RUN apt-get -y install mariadb-server-10.3 mariadb-client

RUN git config --global user.email "bdhwan@gmail.com"
RUN git config --global user.name "bdhwan"

RUN sudo apt-get install -y vim


