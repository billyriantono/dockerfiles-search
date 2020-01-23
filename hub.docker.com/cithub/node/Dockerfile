FROM ubuntu:16.04
MAINTAINER hpatel@channelit.biz
ENV\
	ENV=development
RUN\
	apt-get update &&\
	apt-get install -y vim curl wget sudo default-jdk lsof git ntp &&\
	apt-get update &&\
	apt-get clean &&\
	apt-get -y upgrade
RUN curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash -
RUN sudo apt-get install -y nodejs openssh-server
RUN npm install -g watchman
RUN npm install -g angular-cli
RUN npm install -g typescript
RUN mkdir /var/run/sshd
RUN echo 'root:root' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

RUN touch start.sh &&\
	echo "#!/usr/bin/env bash" >> start.sh &&\
	echo "ng serve --host 0.0.0.0 --port 4200" >> start.sh &&\
	chmod 755 start.sh

EXPOSE 3000 22
CMD ["/usr/sbin/sshd", "-D"]
