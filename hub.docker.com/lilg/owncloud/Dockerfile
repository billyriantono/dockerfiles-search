FROM owncloud
MAINTAINER lilg <lilg@asiainfo.com>

#chain.pem
#domain.key
RUN mkdir /ssl-cert  \
    && ln -s /etc/apache2/sites-available/default-ssl.conf  /etc/apache2/sites-enabled/000-default-ssl.conf
RUN a2enmod ssl
ADD default-ssl.conf /etc/apache2/sites-available/default-ssl.conf

EXPOSE 443

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["apache2-foreground"]
