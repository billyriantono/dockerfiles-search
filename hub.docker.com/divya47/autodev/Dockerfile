FROM ubuntu:18.10
RUN apt update
RUN apt install -y sudo python3 net-tools git openssh-server
RUN git clone https://github.com/divyajai/devops2.git
RUN cd devops2;python3 dev.py
