FROM drupal 

COPY site/sites /var/www/html/sites/

RUN chown -R www-data:www-data sites && \
    chmod 640 sites/default/settings.php
