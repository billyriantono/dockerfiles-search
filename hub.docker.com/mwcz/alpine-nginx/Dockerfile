FROM alpine
MAINTAINER Michael Clayton <mclayton@redhat.com>

ENV LANG en_US.utf8

RUN apk update
RUN apk add nginx curl

RUN mkdir -p /etc/pki/nginx/{certs,private}

# ADD alpine-nginx.tar.gz /
ADD alpine-nginx/ /

# give nginx user access to some dirs
RUN adduser -D -u 1000 -g 'www' www
RUN mkdir /www
RUN chmod -R 777 /www /var/lib/nginx /var/log/nginx /var/tmp/nginx

# give nginx binary access to 
USER www

EXPOSE 8080

ENTRYPOINT ["/usr/local/bin/start"]
