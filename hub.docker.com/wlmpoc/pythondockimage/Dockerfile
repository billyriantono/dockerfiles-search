FROM ubuntu:14.04 
MAINTAINER Mr.Mohammed Syed 
RUN sudo apt-get update
RUN sudo apt-get install -y wget python-dev libmysqlclient-dev python3.4 python-pip
RUN sudo pip install MySQL-python Flask==0.10.1
RUN mkdir /usr/local/web-app-0.1
RUN wget https://github.com/testwlmorg/testdock/raw/master/web-app/dist/web-app-0.1.tar.gz
RUN mv web-app-0.1.tar.gz /usr/local/web-app-0.1/
RUN tar -zxvf /usr/local/web-app-0.1/web-app-0.1.tar.gz
WORKDIR /usr/local/web-app-0.1/
EXPOSE 5000
