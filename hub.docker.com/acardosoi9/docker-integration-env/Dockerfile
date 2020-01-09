FROM debian:9.6

RUN apt-get update
RUN apt-get install -y apt-transport-https lsb-release ca-certificates wget software-properties-common debconf
RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
RUN echo "deb https://packages.sury.org/php/ stretch main" > /etc/apt/sources.list.d/php.list
RUN apt-get update
RUN apt-get install -y dos2unix curl tree openssh-server vim sudo openssl apt-utils gzip php7.1 samba proftpd postgresql mariadb-server
RUN apt-get autoremove
RUN apt-get clean

ENV VOL_DIR=/etc/i9corp
ENV SMB_DIR=${VOL_DIR}/samba

RUN mkdir -p ${SMB_DIR}

COPY ./tools/start-packages /usr/local/bin/start-packages
RUN dos2unix /usr/local/bin/start-packages \
    && chmod +x /usr/local/bin/start-packages

RUN cp /etc/samba/smb.conf /etc/samba/smb.conf.bkp
COPY  ./samba/smb.conf /etc/samba/smb.conf
RUN dos2unix /etc/samba/smb.conf

VOLUME [ "/etc/i9corp" ]

#SSH
EXPOSE 22
#Proftpd
EXPOSE 21
#Samba
EXPOSE 137/udp
EXPOSE 138/udp
EXPOSE 139
EXPOSE 445
#PostgreSQL
EXPOSE 5432
#MariaDB
EXPOSE 3306

CMD ["/usr/local/bin/start-packages"]
