FROM 1and1internet/ubuntu-16-apache-php-7.1
MAINTAINER Kunger <fssbbskefu@gmail.com>

#Run System Repo Update
RUN apt update -y && apt upgrade -y && apt install transmission transmission-daemon wget -y

#Get Setting File

RUN rm -rf /etc/transmission-daemon/setting.json && curl -o /etc/transmission-daemon/settings.json https://raw.githubusercontent.com/ACGunion/Dcoker/master/Transmission/settings.json

RUN /etc/init.d/transmission-daemon start

EXPOSE 22
EXPOSE 80
EXPOSE 9091
EXPOSE 443
EXPOSE 80
EXPOSE 21
EXPOSE 8388
