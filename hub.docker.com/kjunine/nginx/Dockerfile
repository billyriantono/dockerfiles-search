FROM kjunine/ubuntu:latest
MAINTAINER Daniel Ku "kjunine@gmail.com"
ENV REFRESHED_AT 2014-11-01

RUN apt-get install -y nginx

EXPOSE 80

ENTRYPOINT ["nginx", "-g", "daemon off;"]
