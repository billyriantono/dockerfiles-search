FROM alpine:3.10.1
MAINTAINER ChiefWulf <tim@stephens.cc>

#########################################
##         RUN INSTALL SCRIPT          ##
#########################################

RUN apk add --update supervisor && rm -rf /tmp/* /var/cache/apk/*
RUN mkdir -p /opt/hdhomerun
ADD hdhomerun.conf /etc/
RUN wget -O /opt/hdhomerun/hdhomerun_record_linux http://download.silicondust.com/hdhomerun/hdhomerun_record_linux_beta
RUN chmod +x /opt/hdhomerun/hdhomerun_record_linux
RUN chmod 666 /etc/hdhomerun.conf
ADD supervisord.conf /etc/supervisord.conf

#########################################
##         EXPORTS AND VOLUMES         ##
#########################################

VOLUME /hdhomerun
EXPOSE 65001/udp 65002

ENTRYPOINT ["supervisord", "--nodaemon", "--configuration", "/etc/supervisord.conf"]
