FROM ubuntu:trusty

RUN ln -snf /bin/bash /bin/sh

# Replace apt sources.list to fetch packages from AWS EC2
RUN sed -i 's/archive.ubuntu.com/us-east-1.ec2.archive.ubuntu.com/' /etc/apt/sources.list

# Update and upgrade system
RUN DEBIAN_FRONTEND=noninteractive apt-get -y update && DEBIAN_FRONTEND=noninteractive apt-get -y upgrade

RUN DEBIAN_FRONTEND=noninteractive apt-get -y install nodejs npm

RUN DEBIAN_FRONTEND=noninteractive update-alternatives --install /usr/bin/node node /usr/bin/nodejs 99

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

EXPOSE 8080

ENTRYPOINT ["sh", "bot.sh"]
