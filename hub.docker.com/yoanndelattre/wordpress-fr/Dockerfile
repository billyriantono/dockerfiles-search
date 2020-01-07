FROM yoanndelattre/base:base-debian
LABEL MAINTAINER='Yoann Delattre "github.com/yoanndelattre | twitter.com/yoanndelattre_"'
RUN apt-get update && apt-get upgrade -y && \
      apt-get install -y apache2 php libapache2-mod-php php-cli php-mysql php-dev && \
      /usr/sbin/a2ensite default-ssl && \
      /usr/sbin/a2enmod ssl && \
      rm -fr /etc/apache2/sites-available/apache_deb.conf && \
      rm -fr /var/www/* && \
      rm -fr /tmp/install.log && \
      chown -R www-data:www-data /var/www && \
      ls -lah /var/www
COPY Contents/000-default.conf /etc/apache2/sites-available/
COPY Contents/default-ssl.conf /etc/apache2/sites-available/
RUN apt-get install -y wget unzip && \
      wget -P /var/www/ https://fr.wordpress.org/latest-fr_FR.zip && \
      unzip /var/www/latest-fr_FR.zip -d /var/www/ && \
      rm -fr /var/www/latest-fr_FR.zip && \
      chmod -R 777 /var/www/wordpress && \
      apt-get purge -y wget unzip && \
      apt-get -qy clean && \
      rm -rf /var/lib/apt/lists/*
VOLUME ["/var/www/wordpress"]
EXPOSE 80 443
WORKDIR /var/www/wordpress
CMD apachectl -D FOREGROUND