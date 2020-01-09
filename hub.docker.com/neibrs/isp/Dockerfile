FROM alpine
ENV TIMEZONE Asia/Shanghai
#RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories
RUN apk update && apk upgrade
RUN apk add mariadb mariadb-client \
    apache2 \ 
    apache2-utils \
    curl wget vim htop git \
    tzdata \
    php7-apache2 \
    php7-bcmath \
    php7-cli \
    php7-phar \
    php7-zlib \
    php7-zip \
    php7-bz2 \
    php7-ctype \
    php7-curl \
    php7-pdo_mysql \
    php7-mysqli \
    php7-fileinfo \
    php7-json \
    php7-mcrypt \
    php7-xml \
    php7-dom \
    php7-iconv \
    php7-xdebug \
    php7-session \
    php7-intl \
    php7-gd \
    php7-mbstring \
    php7-apcu \
    php7-opcache \
    php7-tokenizer \
    php7-xmlreader \
    php7-xmlwriter \
    php7-simplexml

RUN curl -sS https://getcomposer.org/installer | \
    php -- --install-dir=/usr/bin --filename=composer
# Install Drupal
RUN rm -rf /var/www/html
ENV DRUPAL_VERSION 20190521
RUN git clone -b 8.8.x https://github.com/drupal/drupal.git /var/www/html

WORKDIR /var/www/html
ENV COMPOSER_PROCESS_TIMEOUT 1200
RUN composer install

# Install Drupal modules
RUN composer require \
  drupal/purge \
  drupal/config_rewrite \
  drupal/config_update \
  drupal/memcache \
  drupal/restui \
  drupal/page_manager \
  drupal/panels \
  drupal/panelizer \
  drupal/default_content \
  drupal/migrate_plus \
  drupal/migrate_source_csv \
  drupal/migrate_source_xls \
  drupal/migrate_tools \
  drupal/xls_serialization \
  drupal/entity_print \
  mikehaertl/phpwkhtmltopdf \
  drupal/charts \
  drupal/r4032login \
  drupal/address \
  drupal/ajax_links_api \
  drupal/block_style_plugins:dev-2.x \
  drupal/conditional_fields \
  drupal/custom_formatters \
  drupal/entity_browser \
  drupal/facets \
  drupal/features \
  drupal/field_formatter_class \
  drupal/field_group \
  drupal/inline_entity_form \
  drupal/pinyin \
  drupal/quicktabs \
  drupal/reference_table_formatter \
  drupal/rules \
  drupal/token \
  drupal/token_filter \
  drupal/views_field_formatter \
  drupal/ajax_links_api \
  drupal/varnish_purge \
  drupal/adminimal_admin_toolbar \
  drupal/coffee \
  drupal/color_field \
  drupal/commerce \
  drupal/commerce_recurring \
  drupal/commerce_paypal \
  drupal/commerce_wechat_pay:1.x-dev \
  drupal/commerce_alipay:1.x-dev \
  drupal/alipay_api \
  drupal/cog \
  drupal/console \
  drush/drush \
  drupal/drush_language \
  kgaut/potx \
  drupal/block_style_plugins \
  drupal/typed_data \
  drupal/geofield \
  drupal/baidu_map \
  drupal/geocoder \
  drupal/computed_field \
  drupal/geolocation \
  drupal/geocoder_autocomplete \
  drupal/block_class \
  drupal/ds \
  drupal/superfish \
  drupal/libraries \
  drupal/commerce_autosku \
  drupal/views_slideshow \
  drupal/views_slideshow_cycle \
  drupal/login_security \
  drupal/smart_ip \
  drupal/if_then_else \
  drupal/purge_purger_http \
  drupal/xhprof \
  drupal/components \
  drupal/cog \
  drupal/easy_breadcrumb \
  drupal/commerce_demo

# Install Drupal site
RUN mkdir -p /var/www/html/sites/default/files && \
  chmod a+rw /var/www/html/sites/default -R && \
  cp /var/www/html/sites/default/default.settings.php /var/www/html/sites/default/settings.php && \
  cp /var/www/html/sites/default/default.services.yml /var/www/html/sites/default/services.yml && \
  chmod a+rw /var/www/html/sites/default/settings.php && \
  chmod a+rw /var/www/html/sites/default/services.yml && \
  chown -R apache:apache /var/www/html/

# install-drupal.sh will setup /var/www/private as file_private_path, create it first
RUN mkdir -p /var/www/private && \
  chown -R apache:apache /var/www/private

# Install varnish_purge
RUN composer require \
  drupal/purge \
  drupal/varnish_purge

# Mysql server config
#COPY files/60-drupal.cnf /etc/mysql/conf.d/60-drupal.cnf

#COPY files/install-drupal.sh install-drupal.sh
#RUN chmod +x install-drupal.sh


#
#    sed -i 's#AllowOverride none#AllowOverride All#' /etc/apache2/httpd.conf && \
#    sed -i 's#Require all denied#Require all granted#' /etc/apache2/httpd.conf && \
#    sed -i 's#^DocumentRoot ".*#DocumentRoot "/var/www/localhost/htdocs"#g' /etc/apache2/httpd.conf && \

# configure timezone, mysql, apache
RUN cp /usr/share/zoneinfo/${TIMEZONE} /etc/localtime && \
    echo "${TIMEZONE}" > /etc/timezone && \
    mkdir -p /run/mysqld && chown -R mysql:mysql /run/mysqld /var/lib/mysql && \
    mysql_install_db --user=mysql --verbose=1 --basedir=/usr --datadir=/var/lib/mysql --rpm > /dev/null && \
    mkdir -p /run/apache2 && chown -R apache:apache /run/apache2 && chown -R apache:apache /var/www/localhost/htdocs/ && \
    sed -i 's#\#LoadModule rewrite_module modules\/mod_rewrite.so#LoadModule rewrite_module modules\/mod_rewrite.so#' /etc/apache2/httpd.conf && \
    sed -i 's#ServerName www.example.com:80#\nServerName localhost:80#' /etc/apache2/httpd.conf && \
    sed -i 's/skip-networking/\#skip-networking/i' /etc/my.cnf.d/mariadb-server.cnf && \
    sed -i '/mariadb\]/a log_error = \/var\/lib\/mysql\/error.log' /etc/my.cnf.d/mariadb-server.cnf && \
    sed -i -e"s/^bind-address\s*=\s*127.0.0.1/bind-address = 0.0.0.0/" /etc/my.cnf.d/mariadb-server.cnf && \
    sed -i '/mariadb\]/a skip-external-locking' /etc/my.cnf.d/mariadb-server.cnf && \
    sed -i '/mariadb\]/a general_log = ON' /etc/my.cnf.d/mariadb-server.cnf && \
    sed -i '/mariadb\]/a general_log_file = \/var\/lib\/mysql\/query.log' /etc/my.cnf.d/mariadb-server.cnf

RUN sed -i 's#display_errors = Off#display_errors = On#' /etc/php7/php.ini && \
    sed -i 's#upload_max_filesize = 2M#upload_max_filesize = 100M#' /etc/php7/php.ini && \
    sed -i 's#post_max_size = 8M#post_max_size = 100M#' /etc/php7/php.ini && \
    sed -i 's#session.cookie_httponly =#session.cookie_httponly = true#' /etc/php7/php.ini && \
    sed -i 's#error_reporting = E_ALL & ~E_DEPRECATED & ~E_STRICT#error_reporting = E_ALL#' /etc/php7/php.ini
#ADD entry.sh /entry.sh
#RUN chmod u+x /entry.sh

WORKDIR /var/www/html
EXPOSE 80 22 443 3306
#ENTRYPOINT ["/entry.sh"]
