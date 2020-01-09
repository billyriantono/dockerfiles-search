FROM nginx

MAINTAINER soheil Jahanshahi <s.jahanshahi@developers.nl>

RUN mkdir /etc/nginx/logs && touch /etc/nginx/logs/static.log

ADD ./nginx.conf /etc/nginx/conf.d/default.conf
ADD /src /www