FROM ubuntu:14.04

RUN apt-get update
RUN apt-get install -y nginx

RUN echo 'Hi, Running .. a new <h1> dynamic test container creation </h1>' \
	> /usr/share/nginx/html/index.html

CMD nginx -g "daemon off;"

EXPOSE 80


