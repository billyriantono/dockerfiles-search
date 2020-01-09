FROM ubuntu:18.04

RUN apt-get update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y tzdata
RUN ln -fs /usr/share/zoneinfo/Europe/London /etc/localtime
RUN dpkg-reconfigure -f noninteractive tzdata
RUN apt-get install -y php7.2-cli php7.2-xml php7.2-zip nodejs npm git composer
RUN npm install -g yarn
RUN apt-get install -y openssh-server mariadb-client
RUN /etc/init.d/ssh start
