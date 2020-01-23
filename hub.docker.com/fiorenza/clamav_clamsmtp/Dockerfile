FROM debian:testing
MAINTAINER Fiorenza

# Debian Base to use
ENV DEBIAN_VERSION buster
ENV LISTEN 172.18.0.2:20024
ENV OUT 172.18.0.1:20025
ENV CLAMSMTPUSER clamav
#
# Aggiorno pacchetti
#

# initial install of av daemon
RUN echo "deb http://http.debian.net/debian/ $DEBIAN_VERSION main contrib non-free" > /etc/apt/sources.list && \
    echo "deb http://http.debian.net/debian/ $DEBIAN_VERSION-updates main contrib non-free" >> /etc/apt/sources.list && \
    echo "deb http://security.debian.org/ $DEBIAN_VERSION/updates main contrib non-free" >> /etc/apt/sources.list && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y -qq \
        clamav-daemon \
        clamav-freshclam \
        clamsmtp \
        libclamunrar7 \
        wget && \
        apt-get clean

#rm -rf /var/lib/apt/lists/*

# initial update of av databases
RUN wget -O /var/lib/clamav/main.cvd http://database.clamav.net/main.cvd && \
    wget -O /var/lib/clamav/daily.cvd http://database.clamav.net/daily.cvd && \
    wget -O /var/lib/clamav/bytecode.cvd http://database.clamav.net/bytecode.cvd


# permission juggling

RUN mkdir /var/run/clamsmtp
RUN chown clamav:clamav /var/run/clamsmtp
RUN chmod 750 /var/run/clamsmtp 

# av configuration update
#RUN sed -i 's/^LogSyslog .*$/LogSyslog false/g' /etc/clamav/clamd.conf
#RUN sed -i 's/^LogSyslog .*$/LogSyslog false/g' /etc/clamav/freshclam.conf
#RUN sed -i 's/^Checks .*$/Checks 24/g' /etc/clamav/freshclam.conf

# initial update of av databases
RUN wget -O /var/lib/clamav/main.cvd http://database.clamav.net/main.cvd
RUN wget -O /var/lib/clamav/daily.cvd http://database.clamav.net/daily.cvd
RUN wget -O /var/lib/clamav/bytecode.cvd http://database.clamav.net/bytecode.cvd

# volume provision
VOLUME ["/var/lib/clamav"]
VOLUME ["/var/log/clamav"]

# port provision
EXPOSE 20024

# av daemon bootstrapping
ADD bootstrap.sh /
RUN chmod 755 /bootstrap.sh
ADD clamd.conf /etc/clamav/
ADD freshclam.conf /etc/clamav/
#ADD clamsmtpd.conf /etc
ADD gestionelogclam.sh /etc/cron.d/
RUN chmod 755 /etc/cron.d/gestionelogclam.sh

CMD ["/bootstrap.sh"]