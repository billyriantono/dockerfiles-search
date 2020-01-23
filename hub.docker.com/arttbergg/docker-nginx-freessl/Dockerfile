FROM nginx

RUN echo "deb http://ftp.debian.org/debian jessie-backports main" >> /etc/apt/sources.list
RUN echo "deb http://ftp.debian.org/debian stretch-backports main" >> /etc/apt/sources.list
RUN apt-get update
RUN apt-get -y install cron
RUN echo "0 0 * * 1 certbot renew" >> /var/spool/cron/crontabs/root
RUN echo "" >> /var/spool/cron/crontabs/root

RUN apt-get -y install python-certbot-nginx -t stretch-backports

