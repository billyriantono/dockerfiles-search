FROM alpine:latest 
MAINTAINER info@secops.tech 

RUN apk --no-cache add \
    squid \
    apache2-utils

ADD squid.conf /etc/squid/squid.conf
ADD htpwds /etc/squid/htpwds

EXPOSE 3128

CMD squid -N -X
