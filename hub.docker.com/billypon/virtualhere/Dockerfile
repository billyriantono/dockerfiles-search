FROM alpine:3.7
MAINTAINER billypon

ADD vhusbd /usr/sbin/
ADD config.ini /etc/virtualhere/
ADD on* /etc/virtualhere/

RUN wget http://www.virtualhere.com/sites/default/files/usbserver/vhusbdx86_64 -P /usr/sbin/ && \
    chmod +x /usr/sbin/vhusbdx86_64

EXPOSE 7575
CMD ["vhusbd"]
