FROM debian:9.6

RUN echo "deb http://ftp.debian.org/debian stretch-backports main" >> /etc/apt/sources.list

RUN apt-get update
RUN apt-get install -y python-certbot-apache -t stretch-backports
RUN apt-get install -y dos2unix openssh-server vim sudo apache2 openssl samba
RUN apt-get autoremove
RUN apt-get clean

ENV VOL_DIR=/etc/i9corp
ENV DIST_DIR=${VOL_DIR}/download/dist
ENV SSL_DIR=${VOL_DIR}/config/ssl

ARG BUILD_PASSWD=123456
ARG BUILD_LOGIN=build
ARG SRV_NAME=localhost.com

RUN mkdir -p ${DIST_DIR}
RUN mkdir -p ${SSL_DIR}
RUN mkdir -p .cache

COPY ./tools/start-packages /usr/local/bin/start-packages
RUN dos2unix /usr/local/bin/start-packages \
    && chmod +x /usr/local/bin/start-packages

COPY ./tools/create-certs /usr/local/bin/create-certs
RUN dos2unix /usr/local/bin/create-certs \
    && chmod +x /usr/local/bin/create-certs

RUN cp /etc/samba/smb.conf /etc/samba/smb.conf.bkp
COPY  ./samba/smb.conf /etc/samba/smb.conf
RUN dos2unix /etc/samba/smb.conf

COPY ./apache/repo-windows.conf /etc/apache2/sites-available/repo-windows.conf
RUN dos2unix /etc/apache2/sites-available/repo-windows.conf

COPY ./apache/apache2.conf /etc/apache2/apache2.conf
RUN dos2unix /etc/apache2/apache2.conf

RUN echo "0 0 1 * * root certbot renew --dry-run" >> /etc/crontab

RUN apache2ctl configtest
RUN a2enmod ssl
RUN a2ensite default-ssl

RUN unlink /etc/apache2/sites-enabled/000-default.conf
RUN rm -fr /etc/apache2/sites-available/000-default.conf
RUN ln -s /etc/apache2/sites-available/repo-windows.conf /etc/apache2/sites-enabled/repo-windows.conf

VOLUME [ "/etc/i9corp" ]

#SSH
EXPOSE 22
#Apache/SSL
EXPOSE 443
EXPOSE 80
#Samba
EXPOSE 137/udp
EXPOSE 138/udp
EXPOSE 139
EXPOSE 445

CMD ["/usr/local/bin/start-packages"]
