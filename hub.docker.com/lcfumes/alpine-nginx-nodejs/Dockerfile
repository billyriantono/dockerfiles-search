FROM alpine:3.3 
MAINTAINER Luiz Fumes <luiz.fumes@dafiti.com.br>

#Update and Intalation Ubuntu Packages
RUN apk update && \
    apk upgrade && \
    apk add --update \
            nginx \
            nodejs

WORKDIR /srv/www
ADD . /srv/www

#Commands
CMD exec nginx

#Port
EXPOSE 80
