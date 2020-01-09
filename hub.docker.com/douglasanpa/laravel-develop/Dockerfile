FROM codercom/code-server:v2

RUN sudo apt-get update && \
    sudo DEBIAN_FRONTEND=noninteractive apt-get -y install php php-gd php-mbstring php-xml php-zip apache2 libapache2-mod-php php-mysql nano gcc g++ make libpng-dev dh-autoreconf libpng++-dev pkg-config autoconf libtool nasm unzip php-curl mysql-client && \
    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add - && \
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list && \
    curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash - && \
    sudo apt-get update && \
    sudo apt-get -y install nodejs yarn && \
    curl -sS https://getcomposer.org/installer | php && \
    sudo mv composer.phar /usr/local/bin/composer && \
    sudo chmod +x /usr/local/bin/composer && \
    sudo apache2ctl stop
RUN sudo bash -c "echo '<VirtualHost *:80>' > /etc/apache2/sites-available/000-default.conf" && \
    sudo bash -c "echo '    ServerAdmin webmaster@localhost' >> /etc/apache2/sites-available/000-default.conf" && \
    sudo bash -c "echo '    DocumentRoot /home/coder/project/public' >> /etc/apache2/sites-available/000-default.conf" && \
    sudo bash -c "echo '    <Directory /home/coder/project/public>' >> /etc/apache2/sites-available/000-default.conf" && \
    sudo bash -c "echo '        Options Indexes FollowSymLinks MultiViews' >> /etc/apache2/sites-available/000-default.conf" && \
    sudo bash -c "echo '        AllowOverride All' >> /etc/apache2/sites-available/000-default.conf" && \
    sudo bash -c "echo '        Order allow,Deny' >> /etc/apache2/sites-available/000-default.conf" && \
    sudo bash -c "echo '        Allow from All' >> /etc/apache2/sites-available/000-default.conf" && \
    sudo bash -c "echo '    </Directory>' >> /etc/apache2/sites-available/000-default.conf" && \
    sudo bash -c "echo '    ErrorLog \${APACHE_LOG_DIR}/error.log' >> /etc/apache2/sites-available/000-default.conf" && \
    sudo bash -c "echo '    CustomLog \${APACHE_LOG_DIR}/access.log combined' >> /etc/apache2/sites-available/000-default.conf" && \
    sudo bash -c "echo '</VirtualHost>' >> /etc/apache2/sites-available/000-default.conf" && \
    sudo sed -i -e \
    's/\/var\/www\// \/home\/coder\/project\//g' \
    /etc/apache2/apache2.conf && \
    sudo sed -i -e \
    's/www-data/coder/g' \
    /etc/apache2/envvars && \
    sudo a2enmod rewrite && \
    sudo bash -c "echo 'export PATH=\"\$PATH:/home/coder/project/vendor/bin\"' >> /home/coder/.bashrc"

    
ENV APP_NAME Laravel
ENV DB_HOST mariadb
ENV DB_PORT 3306
ENV DB_DATABASE laravel
ENV DB_USERNAME laravel
ENV APP_ENV local
COPY wait-for-it.sh start.sh /
RUN sudo chmod +x /wait-for-it.sh && \
    sudo chmod +x /start.sh

EXPOSE 80
EXPOSE 443

ENTRYPOINT /wait-for-it.sh $DB_HOST:$DB_PORT --strict --timeout=120 -- /start.sh








