FROM ubuntu:latest

MAINTAINER santoshreddy<santoshreddy@linex.in>

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10 && ap-get update && aptitude install -y apache

EXPOSE 80

CMD ["service apache start"]



