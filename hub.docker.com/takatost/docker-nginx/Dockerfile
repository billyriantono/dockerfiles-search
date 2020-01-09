FROM nginx:1.13.1-alpine

MAINTAINER JohnWang <i@takato.st>

COPY nginx.conf /etc/nginx/nginx.conf

RUN rm -f /var/log/nginx/access.log
RUN rm -f /var/log/nginx/error.log
