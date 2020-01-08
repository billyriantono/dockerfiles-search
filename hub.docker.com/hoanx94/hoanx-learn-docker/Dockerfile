FROM ubuntu:16.04
MAINTAINER hoanguyen.contact@gmail.com
RUN DEBIAN_FRONTEND=noninteractive
RUN apt-get update
RUN apt-get install -y nginx
WORKDIR /venv
COPY start.sh /venv
RUN chmod a+x /venv/*
ENTRYPOINT ["/venv/start.sh"] 
EXPOSE 80
