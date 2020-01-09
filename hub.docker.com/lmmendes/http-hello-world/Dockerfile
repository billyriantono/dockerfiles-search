FROM alpine
MAINTAINER lmmendes
RUN apk --no-cache add nginx &&\
  mkdir -p /run/nginx &&\
  mkdir -p /var/www/html
ADD nginx.conf /etc/nginx/
ADD index.html /var/www/html
EXPOSE 80
CMD ["nginx"]
