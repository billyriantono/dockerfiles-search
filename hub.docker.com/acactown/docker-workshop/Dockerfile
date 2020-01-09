FROM ubuntu:12.04

MAINTAINER Andres Amado "acactown@gmail.com"

RUN apt-get update
RUN apt-get install -y nginx zip curl

RUN echo "daemon off;" >> /etc/nginx/nginx.conf
RUN curl -o /usr/share/nginx/www/master.zip -L https://s3.amazonaws.com/docker-workshop/2048-master.zip
RUN cd /usr/share/nginx/www/ && unzip master.zip && mv 2048-master/* . && rm -rf 2048-master master.zip

ENV JAVA_HOME /usr/local/java

EXPOSE 80

USER root

WORKDIR /tmp

CMD ["/usr/sbin/nginx", "-c", "/etc/nginx/nginx.conf"]
