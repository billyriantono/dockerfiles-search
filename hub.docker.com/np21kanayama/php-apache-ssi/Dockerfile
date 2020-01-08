FROM php:apache

RUN { \
echo 'LoadModule include_module /usr/lib/apache2/modules/mod_include.so'; \
echo ''; \
echo 'ServerName piyopiyo:80'; \
echo '<Directory /var/www/>'; \
echo 'Options +Indexes +Includes +FollowSymLinks'; \
echo 'AddType text/html .html .php'; \
echo 'AddOutputFilter INCLUDES .html .php'; \
echo '</Directory>'; \
} | tee "$APACHE_CONFDIR/conf-available/ssi.conf" \
&& a2enconf ssi

EXPOSE 80
CMD ["apache2-foreground"]