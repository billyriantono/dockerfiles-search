FROM debian:jessie
MAINTAINER Daniel Delgado <daniel@nettalk.com>

USER root
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y apache2 asterisk vim tcpdump net-tools
RUN apt-get update && apt-get install -y unixODBC unixODBC-dev libmyodbc libav-tools

# backup original files
RUN cp /etc/asterisk/asterisk.conf /etc/asterisk/asterisk.conf.bk
RUN cp /etc/asterisk/sip.conf /etc/asterisk/sip.conf.bk
RUN cp /etc/asterisk/extconfig.conf /etc/asterisk/extconfig.conf.bk
RUN cp /etc/asterisk/extensions.conf /etc/asterisk/extensions.conf.bk

COPY entrypoint.sh /entrypoint.sh
COPY extensions_nettalk.conf /etc/asterisk/extensions_nettalk.conf
COPY sip_nettalk.conf /etc/asterisk/sip_nettalk.conf
COPY extconfig.conf /etc/asterisk/extconfig.conf
COPY extensions.conf /etc/asterisk/extensions.conf
COPY sip.conf /etc/asterisk/sip.conf
COPY asterisk.conf /etc/asterisk/asterisk.conf
COPY odbcinst.ini /etc/odbcinst.ini
COPY odbc.ini /etc/odbc.ini

RUN odbcinst -q -d

CMD ["/usr/sbin/asterisk", "-f"]
