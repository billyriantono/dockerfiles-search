FROM nginx

MAINTAINER TSoftware

ADD / /webapp

RUN cd /webapp && rm -v /etc/nginx/nginx.conf && cp nginx/nginx.conf /etc/nginx/