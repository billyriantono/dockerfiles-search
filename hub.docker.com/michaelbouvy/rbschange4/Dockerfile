FROM        debian:wheezy
MAINTAINER  Michael BOUVY <michael.bouvy@gmail.com>

ADD         https://getcomposer.org/composer.phar /usr/local/bin/composer
RUN         chmod +x /usr/local/bin/composer
RUN         apt-get update && DEBIAN_FRONTEND=noninteractive apt-get -y install php5 php5-intl php5-json php5-sqlite \ 
            libapache2-mod-php5 git-core php5-curl php5-gd php5-xsl php5-imagick php5-mcrypt supervisor openssh-server

RUN         echo "root:toor" | chpasswd

RUN         mkdir -p /var/run/sshd /var/log/supervisor

RUN         php /usr/local/bin/composer --stability=dev --no-interaction create-project rbschange/change c4

RUN         mv c4 /var/www/ ; cd /var/www/c4 ; mkdir -p App/Config bin; \
            cp ChangeTests/travisconfig/config/project.sqlite.json App/Config/project.json ; \
            sed -i -e 's/ChangeTests\/UnitTestWorkspace\///g' App/Config/project.json ; \
            mkdir www ; chown -R www-data:www-data /var/www/

#ADD         http://www.rbschange.fr/static/change.phar /var/www/c4/bin/
ADD         change.phar /var/www/c4/bin/
            
RUN         cd /var/www/c4 ; \
            php bin/change.phar change:set-document-root www ; \
            php bin/change.phar change:generate-db-schema ; \
            php bin/change.phar change:register-plugin --all ; \
            php bin/change.phar change:install-package --vendor=Rbs Core ; \
            php bin/change.phar change:install-package --vendor=Rbs ECom ; \
            php bin/change.phar change:install-plugin --type=theme --vendor=Rbs Demo ; \
            php bin/change.phar rbs_user:add-user admin-change@bobmail.info admin --realms=Rbs_Admin,web --is-root=true --password=admin ; \
            php bin/change.phar change:compile-i18n
            
RUN         chown -R www-data:www-data /var/www/

ADD         apache-c4-vhost.conf /etc/apache2/sites-available/001-c4
RUN         a2ensite 001-c4 ; a2dissite 000-default
            
ADD         supervisord.conf /etc/supervisor/conf.d/supervisord.conf

EXPOSE      22 80
CMD         ["/usr/bin/supervisord"]
