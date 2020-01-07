FROM debian:latest

LABEL Description="Debian base image"
MAINTAINER Devis Lucato <https://github.com/dluc>

COPY ./install /root/install

RUN apt-get update && \
  apt-get install -y --no-install-recommends --show-progress \
    apt-listchanges apt-utils bash-completion bindechexascii bsdmainutils bsdutils \
    bzip2 ca-certificates curl dnsutils findutils gettext git htop jq less logrotate \
    man mc nano netbase nmap net-tools netcat-traditional nmap ntp psmisc rsync \
    rsyslog screen sed strace telnet tree traceroute unzip wget whois zip \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* && \
  cp /root/install/etc/resolv.conf  /etc/   && chmod 644 /etc/resolv.conf && \
  cp /root/install/etc/timezone     /etc/   && chmod 644 /etc/timezone && \
  cp /root/install/home/.screenrc   /root/  && chmod 640 /root/.screenrc && \
  cp /root/install/home/.bashcustom /root/  && chmod 640 /root/.bashcustom && \
  echo "" >> /root/.bashrc && echo "source ~/.bashcustom" >> /root/.bashrc && \
  rm -fR /root/install

CMD service rsyslog start; service cron start; /bin/bash