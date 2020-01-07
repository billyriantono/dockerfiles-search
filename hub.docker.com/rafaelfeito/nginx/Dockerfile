FROM debian:jessie

MAINTAINER Rafael MF <rafael.feito@gmail.com>

RUN echo "deb http://mirror.ufpa.br/debian jessie main contrib" > /etc/apt/sources.list
RUN apt-get update && apt-get install -y nginx 

EXPOSE 80

ENTRYPOINT ["nginx", "-g", "daemon off;"]
