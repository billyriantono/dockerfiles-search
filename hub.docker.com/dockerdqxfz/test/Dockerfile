# Version: 0.0.1
FROM ubuntu:14.04
MAINTAINER wengyang "1612487591@qq.com"
#RUN apt-get update && apt-get install -y nginx
#RUN echo 'Hi, I am in your container' \
#	>/usr/share/nginx/html/index.html
#EXPOSE 80
WORKDIR /root
RUN touch blank02
WORKDIR /root
ENTRYPOINT ["/bin/sh","-c","while true; do echo world; sleep 1; done"]

