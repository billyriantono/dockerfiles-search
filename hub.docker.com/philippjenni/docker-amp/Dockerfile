FROM philippjenni/docker-mysql

MAINTAINER Philipp Jenni <philippjenni@bluemail.ch>

RUN apt-get -y update

# Install needed software
RUN DEBIAN_FRONTEND=noninteractive apt-get -y --force-yes install apache2 libapache2-mod-php php-mysql php7.0-sqlite3 php-gd software-properties-common

# Install Java.
RUN \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get update && \
  apt-get install -y oracle-java8-installer && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /var/cache/oracle-jdk8-installer

# Enable apache mods.
RUN a2enmod php7.0
RUN a2enmod rewrite

# php config
RUN sed -i -e "s/post_max_size\s*=\s*8M/post_max_size = 16M/g" /etc/php/7.0/apache2/php.ini
RUN sed -i -e "s/upload_max_filesize\s*=\s*2M/upload_max_filesize = 16M/g" /etc/php/7.0/apache2/php.ini
RUN sed -i -e "s/short_open_tag\s*=\s*Off/short_open_tag = On/g" /etc/php/7.0/apache2/php.ini
RUN sed -i -e "s/;date.timezone\s*=\s*/date.timezone = Europe\/Zurich/g" /etc/php/7.0/apache2/php.ini

# Manually set up the apache environment variables
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2
ENV APACHE_LOCK_DIR /var/lock/apache2
ENV APACHE_PID_FILE /var/run/apache2.pid
ENV WWW_ROOT /var/www/site

# Update the default apache site with the config we created.
ADD apache-config.conf /etc/apache2/sites-enabled/000-default.conf

# Copy site into place.
ADD www $WWW_ROOT
# Giving rights to user www-data to data dir of application
RUN chown -R www-data $WWW_ROOT

# Add start script
ADD ./startScripts/start-amp.sh /startScripts/start-amp.sh
RUN chmod 755 /startScripts/start-amp.sh

CMD ["/startScripts/start-amp.sh"]