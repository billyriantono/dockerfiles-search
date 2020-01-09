FROM ubuntu:16.04
RUN apt update &&\
    apt install -y sudo vim &&\
    touch /root/.bashrc &&\
    echo "export PS1='\h:\w\\\$ '" >> /root/.bashrc &&\
    echo "alias r='fc -e -'" >> /root/.bashrc &&\
    echo "set -o vi" >> /root/.bashrc
