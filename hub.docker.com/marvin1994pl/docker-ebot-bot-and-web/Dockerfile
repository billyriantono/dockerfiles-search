FROM debian:jessie

ENV EBOT_HOME="/ebot" TIMEZONE="Europe/Warsaw" WWW="/var/www/html" NEW_WWW="$EBOT_HOME/web/web"

RUN apt-get update && apt-get -y upgrade && apt-get clean

RUN apt-get -y install sudo curl git php5-cli php5-mysql libapache2-mod-php5 && apt-get clean

#RUN curl -sL https://deb.nodesource.com/setup_5.x | sudo bash -
RUN apt-get install -y nodejs npm && apt-get clean
RUN /bin/ln -s /usr/bin/nodejs /usr/bin/node

RUN sed -i "s~;date.timezone =~date.timezone = $TIMEZONE~g" /etc/php5/cli/php.ini
RUN echo 'extension=pthreads.so' >> /etc/php5/cli/php.ini

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin

RUN mkdir "$EBOT_HOME" && mkdir "$EBOT_HOME/bot" && mkdir "$EBOT_HOME/web"
RUN git clone https://github.com/deStrO/eBot-CSGO.git "$EBOT_HOME/bot"
RUN git clone https://github.com/deStrO/eBot-CSGO-Web.git "$EBOT_HOME/web"
RUN cd "$EBOT_HOME/web" && cp config/app_user.yml.default config/app_user.yml
RUN cd "$EBOT_HOME/bot" && /usr/bin/php /usr/bin/composer.phar install && npm install socket.io formidable archiver

RUN a2enmod rewrite

RUN sed -i 's/MYSQL_IP = "127.0.0.1"/MYSQL_IP = "5.135.147.191"/g' $EBOT_HOME/bot/config/config.ini
RUN sed -i 's/127.0.0.1/localhost/g' $EBOT_HOME/bot/config/config.ini
RUN sed -i 's/MYSQL_USER = "ebotv3"/MYSQL_USER = "marvin_eBot"/g' $EBOT_HOME/bot/config/config.ini
RUN sed -i 's/MYSQL_PASS = "ebotv3"/MYSQL_PASS = "dJwfxHTdoM"/g' $EBOT_HOME/bot/config/config.ini
RUN sed -i 's/MYSQL_BASE = "ebotv3"/MYSQL_BASE = "marvin_eBot"/g' $EBOT_HOME/bot/config/config.ini

RUN sed -i 's/$WWW/$NEW_WWW/g' /etc/apache2/sites-enabled/000-default.conf
RUN sed -i 's/$WWW/$NEW_WWW/g' /etc/apache2/sites-available/000-default.conf

RUN sed -i 's/dsn:      mysql:host=localhost;dbname=ebotv3/dsn:      mysql:host=5.135.147.191;dbname=marvin_eBot/g' $EBOT_HOME/web/config/databases.yml
RUN sed -i 's/username: root/username: marvin_eBot/g' $EBOT_HOME/web/config/databases.yml
RUN sed -i 's/password: /password: dJwfxHTdoM/g' $EBOT_HOME/web/config/databases.yml

RUN apt-get update && apt-get -y upgrade && apt-get clean

COPY Match.php $EBOT_HOME/bot/src/eBot/Match/Match.php

VOLUME ["$EBOT_HOME/bot/demos", "$EBOT_HOME/bot/logs", "$EBOT_HOME/bot/config", "$EBOT_HOME/web/config" , "/etc/apache2"]

EXPOSE 80

#RUN cd $EBOT_HOME/web ; php symfony configure:database 'mysql:host=5.135.147.191;dbname=marvin_eBot' marvin_eBot dJwfxHTdoM ; php symfony cc ; apachectl -d /etc/apache2 -f /etc/apache2/apache2.conf -e debug -DFOREGROUND"]
CMD ["sh", "-c", "screen -dmS ebotv3 php $EBOT_HOME/bot/bootstrap.php"]
