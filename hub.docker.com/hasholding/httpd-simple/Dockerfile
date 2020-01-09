FROM alpine:3.7

LABEL maintainer "Levent SAGIROGLU <LSagiroglu@gmail.com>"

RUN apk add --update --no-cache ca-certificates apache2 && \	
    update-ca-certificates
ADD index.html /var/www/localhost/htdocs
RUN mkdir -p /run/apache2  
RUN echo "ServerName localhost" >> /etc/apache2/httpd.conf
CMD ["httpd", "-D", "FOREGROUND"]