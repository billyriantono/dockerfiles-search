FROM alpine:3.9

# Install Apache, PHP, and various development tools.
RUN apk add --no-cache \
  apache2 \
  bash \
  ca-certificates \
  curl \
  git \
  gzip \
  jq \
  mysql-client \
  nodejs \
  nodejs-npm \
  patch \
  php7 \
  php7-apache2 \
  php7-bcmath \
  php7-bz2 \
  php7-calendar \
  php7-ctype \
  php7-curl \
  php7-dba \
  php7-dom \
  php7-exif \
  php7-fileinfo \
  php7-ftp \
  php7-gd \
  php7-gettext \
  php7-iconv \
  php7-imap \
  php7-json \
  php7-ldap \
  php7-mbstring \
  php7-mysqli \
  php7-mysqlnd \
  php7-odbc \
  php7-opcache \
  php7-openssl \
  php7-pdo \
  php7-pdo_mysql \
  php7-pdo_odbc \
  php7-pdo_pgsql \
  php7-pdo_sqlite \
  php7-pecl-apcu \
  php7-pecl-mcrypt \
  php7-pecl-memcached \
  php7-pgsql \
  php7-phar \
  php7-posix \
  php7-pspell \
  php7-recode \
  php7-shmop \
  php7-simplexml \
  php7-soap \
  php7-sockets \
  php7-sqlite3 \
  php7-sysvmsg \
  php7-sysvsem \
  php7-sysvshm \
  php7-tidy \
  php7-tokenizer \
  php7-wddx \
  php7-xdebug \
  php7-xml \
  php7-xmlreader \
  php7-xmlrpc \
  php7-xmlwriter \
  php7-xsl \
  php7-zip \
  php7-zlib \
  rsync \
  sudo \
  tar \
  unzip \
  vim \
  wget \
  zip

# Configure PHP.
COPY conf/php.ini conf/php-cli.ini /etc/php7/

# Configure Apache.
COPY conf/docker-apache.conf /etc/apache2/conf.d/
EXPOSE 80
RUN mkdir -p /run/apache2 && \
  mkdir -p /var/www/html

# Add scripts.
COPY scripts/* /usr/local/bin/
RUN chmod +x /usr/local/bin/apache2-foreground && \
  chmod +x /usr/local/bin/build-and-test && \
  chmod +x /usr/local/bin/build-project && \
  chmod +x /usr/local/bin/docker-drupaldev-entrypoint && \
  chmod +x /usr/local/bin/export-buildvars && \
  chmod +x /usr/local/bin/fix-project-permissions && \
  chmod +x /usr/local/bin/install-and-test && \
  chmod +x /usr/local/bin/install-composer && \
  chmod +x /usr/local/bin/install-drupal

# Install Composer.
RUN install-composer && mv composer.phar /usr/local/bin/composer

# Install Grunt.
RUN npm install -g grunt-cli

# Install Gulp.
RUN npm install -g gulp-cli

# Configure Drush.
RUN mkdir -p /etc/drush
COPY conf/drushrc.php /etc/drush/

# Create a user for running commands.
# To avoid file permission issues in our CI environment, we set the UID and GID
# to match the bamboo service user on dev.ur.wmich.edu.
RUN addgroup -g 1003 -S drupaldev && \
  adduser -u 1003 -G drupaldev -S drupaldev && \
  adduser drupaldev www-data && \
  echo "drupaldev ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers.d/docker && \
  chmod 0440 /etc/sudoers.d/docker

# Set up the mount point for the project.
RUN mkdir -p /opt/project
VOLUME /opt/project

# Set up the web root for Drupal.
RUN mkdir -p /var/www/html/sites/all/modules/contrib && \
  mkdir -p /var/www/html/sites/all/modules/wmu && \
  mkdir -p /var/www/html/sites/all/libraries && \
  mkdir -p /var/www/html/sites/default/files && \
  mkdir -p /var/www/private-files && \
  chown -R drupaldev:drupaldev /var/www/html && \
  chown drupaldev:www-data /var/www/html/sites/default/files && \
  chmod 2775 /var/www/html/sites/default/files && \
  chown drupaldev:www-data /var/www/private-files && \
  chmod 2775 /var/www/private-files
VOLUME /var/www/html

# Set environment defaults for scripts.
ENV WEB_ROOT /var/www/html
ENV VENDOR_DIR /opt/project/vendor
ENV PATH ${PATH}:${VENDOR_DIR}/bin
ENV MYSQL_HOST db
ENV MYSQL_DATABASE drupal
ENV MYSQL_USER drupal
ENV MYSQL_PASSWORD drupal
ENV DRUPAL_USER drupal
ENV DRUPAL_PASSWORD drupal
ENV DRUPAL_PROFILE minimal
ENV DRUPAL_FILE_PRIVATE_PATH /var/www/private-files
ENV REPORTS_DIR /opt/project/test-reports
ENV BUILDVARS_FILE ${REPORTS_DIR}/buildvars
ENV GRUNT_BUILD_TASK build
ENV GULP_BUILD_TASK build

# Set up the entrypoint.
WORKDIR /opt/project
USER drupaldev
ENTRYPOINT ["docker-drupaldev-entrypoint"]
CMD ["sudo","apache2-foreground"]
