FROM cbolt/webgrind

# Move the applicaiton somewhere else & change the apache config
RUN mv /var/www/html /var/cachegrind && \
sed -i "s@DocumentRoot /var/www/html@DocumentRoot /var/cachegrind@" /etc/apache2/sites-available/000-default.conf && \
echo "<Directory /var/cachegrind/>\n\tOptions Indexes FollowSymLinks\n\tAllowOverride None\n\tRequire all granted\n</Directory>" >> /etc/apache2/apache2.conf
