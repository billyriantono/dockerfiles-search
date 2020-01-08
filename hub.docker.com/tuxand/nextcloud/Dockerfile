FROM nextcloud:latest

RUN apt-get update && apt-get install -y \
  supervisor smbclient \
  && rm -rf /var/lib/apt/lists/* \
  && mkdir /var/log/supervisord /var/run/supervisord

# Fix some smbclient permission errors
RUN chown -R root:www-data /var/run/samba && chmod -R a+xrw /var/run/samba
RUN chown -R root:www-data /var/lib/samba && chmod -R a+xrw /var/lib/samba

COPY supervisord.conf /etc/supervisor/supervisord.conf

RUN echo '*/5 * * * * php /var/www/html/occ preview:pre-generate' >> /var/spool/cron/crontabs/www-data
RUN echo '0 6 1 * * php /var/www/html/occ trashbin:cleanup --all-users' >> /var/spool/cron/crontabs/www-data


ENV NEXTCLOUD_UPDATE=1

CMD ["/usr/bin/supervisord"]
