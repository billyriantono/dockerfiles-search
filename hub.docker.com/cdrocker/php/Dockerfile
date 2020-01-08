FROM alpine:latest
MAINTAINER me codar nl
RUN apk add --update --no-cache php7-fpm php7-session php7-bz2 php7-json php7-openssl php7-sqlite3 \
                      php7-pear php7-tokenizer php7-pdo_mysql php7-sodium php7-xsl php7-mbstring \
                      php7-xmlrpc php7-pdo_sqlite php7-exif php7-gd php7-gettext php7-xml php7-curl \
                      php7-mcrypt php7-mysqli php7-sockets php7-zmq php7-event php7-memcached php7-yaml \
                      php7-soap php7-pdo php7-zip composer php7-opcache s6 ca-certificates zip
COPY files/root/ /
# permissions
RUN		chmod a+x /service/*/run
# http and https
EXPOSE 9000/tcp
# manage with s6
ENTRYPOINT ["/bin/s6-svscan","/service"]
