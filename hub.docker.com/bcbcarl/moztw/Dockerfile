FROM ubuntu:12.04
MAINTAINER Carl X. Su <bcbcarl@gmail.com>

ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2

RUN \
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive RUNLEVEL=1 apt-get install -y apache2 && \
  apt-get clean && rm -rf /var/lib/apt/lists/* && \
  sed -i -e 's|^ULIMIT_MAX_FILES|#ULIMIT_MAX_FILES|' /usr/sbin/apache2ctl && \
  echo "ServerName 0.0.0.0" >> /etc/apache2/conf.d/fqdn && \
  RUNLEVEL=1 a2enmod include

ADD apache2.conf /etc/apache2/sites-available/default
ADD docker-httpd /usr/sbin/docker-httpd

RUN chmod +x /usr/sbin/docker-httpd

EXPOSE 80

ENTRYPOINT ["/bin/bash"]
CMD ["/usr/sbin/docker-httpd"]
