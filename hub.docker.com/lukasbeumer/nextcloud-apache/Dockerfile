FROM nextcloud:apache

RUN apt-get update && apt-get install -y \
  supervisor \
  cron \
  && rm -rf /var/lib/apt/lists/*

RUN mkdir /var/log/supervisord /var/run/supervisord && \ 
  echo "*/15 * * * * su - www-data -s /bin/bash -c \"php -f /var/www/html/cron.php\""| crontab -

RUN a2enmod headers && service apache2 restart

COPY supervisord.conf /etc/supervisor/supervisord.conf
COPY .htaccess /var/www/html/.htaccess

CMD ["/usr/bin/supervisord"]
