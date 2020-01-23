on 0.0.1
FROM ubuntu:14.04
MAINTAINER Chris Weiss "bitblit@gmail.com"
ENV REFRESHED_AT 2015-04-18
RUN apt-get update
RUN apt-get install -y nginx
RUN echo 'Hi, I am in your container' > /usr/share/nginx/html/index.html
EXPOSE 80
ENTRYPOINT ["/usr/sbin/nginx","-g","daemon off;"]
