FROM ubuntu:14.04
MAINTAINER Docker Education Team <education@docker.com>
# adding comment at top hi venkat 
RUN apt-get update
RUN apt-get install -y nginx
RUN echo 'Hi, I am in your container' \
    >/usr/share/nginx/html/index.html

CMD [ "nginx", "-g", "daemon off;" ]
#adding the comment for webhooks
#adding the second line comment for webhook testin.
EXPOSE 80
