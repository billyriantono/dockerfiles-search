  FROM ubuntu

  MAINTAINER Romin Irani (email@domain.com)

  RUN apt-get update

  RUN apt-get install -y nginx

  ENTRYPOINT [“/usr/sbin/nginx”,”-g”,”daemon off;”] # An ENTRYPOINT allows you to configure a container that will run as an executable.

  EXPOSE 80
