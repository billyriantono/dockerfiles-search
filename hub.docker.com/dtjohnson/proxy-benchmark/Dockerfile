FROM debian

RUN apt-get update \
  && apt-get -y install \
    apache2 \
    gettext \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

RUN /usr/sbin/a2enmod proxy_http ssl

COPY 000-default.conf.template /
COPY startup.sh /
COPY cert.pem key.pem /etc/ssl/

RUN chmod +x /startup.sh

CMD ["/startup.sh"]

EXPOSE 80