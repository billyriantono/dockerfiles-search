# version 0.0.1

FROM alexhuang/ubuntu
MAINTAINER Alex Huang "nikshuang@163.com"
ENV REFRESHED 2015-9-6
RUN apt-get update
RUN apt-get install -yq nginx
RUN mkdir -p /var/www/html
ADD global.conf /etc/nginx/conf.d/
ADD nginx.conf /etc/nginx/
EXPOSE 80
