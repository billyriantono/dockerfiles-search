FROM wordpress:latest
# Set environment variables used by the Wordpress image
# DB_USER and DB_PASSWORD are included as an example. However,
# these should be removed and set during docker run.
ENV WORDPRESS_DB_HOST=us-cdbr-iron-east-05.cleardb.net \
    WORDPRESS_DB_USER=bb8af468c8740b \
    WORDPRESS_DB_PASSWORD=d4826a15 \
    WORDPRESS_DB_NAME=heroku_05879b2d87a1f1b \
    WORDPRESS_TABLE_PREFIX=mbet_

COPY plugins/ /var/www/html/wp-content/plugins
COPY uploads/ /var/www/html/wp-content/uploads
# COPY config/ /etc/apache2


# RUN cp -r /usr/src/wordpress/. /var/www/html/