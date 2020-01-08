FROM tekki/sql-ledger:3.2.8.12-e

RUN rm -rf /etc/apache2/sites-* 
COPY sql-ledger-httpd.conf /etc/apache2/sites-available/sql-ledger.conf
RUN set -ex \
  && mkdir -p /etc/apache2/sites-available \
  && mkdir -p /etc/apache2/sites-enabled \
  && a2enmod -q cgid \
  && a2ensite -q sql-ledger

CMD ["/usr/sbin/apache2ctl", "-D", "FOREGROUND"]
