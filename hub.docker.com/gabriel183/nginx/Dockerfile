FROM debian:8

MAINTAINER Gabriel Silva <gabrielp@ufpa.br>

COPY sources.list /etc/apt/sources.list

RUN apt update

RUN apt install -y nginx

EXPOSE 80

ENTRYPOINT ["nginx", "-g", "daemon off;"]
