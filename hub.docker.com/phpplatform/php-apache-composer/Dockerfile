FROM phpplatform/php-apache:5.4

RUN apt-get update -yqq \
    && apt-get install git -yqq \
    && apt-get install wget -yqq \
    && apt-get install zip -yqq \
    && apt-get install unzip -yqq
    
RUN wget https://composer.github.io/installer.sig -O - -q | tr -d '\n' > installer.sig \
    && php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" \
    && php -r "if (hash_file('SHA384', 'composer-setup.php') === file_get_contents('installer.sig')) { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;" \
    && php composer-setup.php \
    && php -r "unlink('composer-setup.php'); unlink('installer.sig');" \
    && mv composer.phar /usr/local/bin/composer

CMD ["apache2-foreground"]