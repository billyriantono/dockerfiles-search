FROM ubuntu:latest

RUN apt-get -y update && apt-get -y upgrade
RUN apt-get -y install nginx

EXPOSE 80

ENTRYPOINT ["nginx", "-g", "daemon off;"]