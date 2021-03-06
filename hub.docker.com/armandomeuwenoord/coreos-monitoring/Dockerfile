FROM debian:sid
MAINTAINER Boris HUISGEN <bhuisgen@hbis.fr>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -y update
RUN apt-get -y upgrade

RUN apt-get -y install locales
RUN dpkg-reconfigure locales && locale-gen C.UTF-8 && /usr/sbin/update-locale LANG=C.UTF-8
RUN echo 'en_US.UTF-8 UTF-8' >> /etc/locale.gen && locale-gen
ENV LC_ALL C.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8

RUN apt-get -y install ucf procps iproute

RUN apt-get -y install supervisor
COPY etc/supervisor/ /etc/supervisor/

COPY files/zabbix-agent_2.4.3-1+wheezy_amd64.deb /root/
RUN apt-get -y install --no-install-recommends pciutils libcurl3-gnutls libldap-2.4-2 cron curl jq netcat-openbsd sudo vim
RUN dpkg -i /root/zabbix-agent_2.4.3-1+wheezy_amd64.deb
COPY etc/zabbix/ /etc/zabbix/
COPY etc/sudoers.d/zabbix etc/sudoers.d/zabbix
RUN chmod 400 /etc/sudoers.d/zabbix
COPY etc/zabbix/crontab /var/spool/cron/crontabs/zabbix
RUN chmod 600 /var/spool/cron/crontabs/zabbix
RUN chown zabbix:crontab /var/spool/cron/crontabs/zabbix

COPY run.sh /
RUN chmod +x /run.sh

EXPOSE 10050
ENTRYPOINT ["/run.sh"]
CMD [""]
