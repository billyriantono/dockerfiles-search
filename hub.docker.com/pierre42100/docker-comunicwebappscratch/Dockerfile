FROM ubuntu:bionic
LABEL Description="Image used to deploy / test ComunicWebApp"
ENV DEBIAN_FRONTEND="noninteractive" HOME="/"

RUN apt update && apt upgrade -y
RUN apt install git php7.2 uglifyjs apache2 libapache2-mod-php7.2 zip -y

#Fix timezone
RUN echo "Europe/Paris" > /etc/timezone; dpkg-reconfigure -f noninteractive tzdata
