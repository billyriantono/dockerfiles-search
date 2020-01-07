FROM ubuntu:latest
MAINTAINER Takumu Uyama
RUN apt-get update && apt-get -y upgrade && apt-get -y install software-properties-common tzdata && echo "mysql-server-5.7 mysql-server/root_password password password" | debconf-set-selections && echo "mysql-server-5.7 mysql-server/root_password_again password password" | debconf-set-selections
RUN apt-get -y install wget mysql-server git
RUN cd ~ && wget https://storage.googleapis.com/golang/go1.8.3.linux-amd64.tar.gz && tar xf go1.8.3.linux-amd64.tar.gz && mv go /usr/local/go1.8.3 && ln -s /usr/local/go1.8.3 /usr/local/go && mkdir go && echo 'export GOPATH="$HOME/go"\nexport PATH="/usr/local/go/bin:$GOPATH/bin:$PATH"' >> .bashrc
