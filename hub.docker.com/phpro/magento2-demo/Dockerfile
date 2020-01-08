FROM debian:jessie

MAINTAINER Steven Trescinski <steven.trescinski@phpro.be>

# Setting Magento installation variables, these can ben changed if required (rebuild required!)
ENV MAGE_BASE_URL "http://magento2-demo.local/"
ENV MAGE_BACKEND_FRONTNAME "admin"
ENV MAGE_ADMIN_FIRSTNAME "Magento"
ENV MAGE_ADMIN_LASTNAME "User"
ENV MAGE_ADMIN_EMAIL "user@example.com"
ENV MAGE_ADMIN_USER "admin"
ENV MAGE_ADMIN_PASSWORD "password123"
ENV MAGE_LANGUAGE "en_US"
ENV MAGE_CURRENCY "EUR"
ENV MAGE_TIMEZONE "Europe/Brussels"

# Adding environment TAG of the Git project, should you want to install another TAG version simply change this environment variable (rebuild required!)
ENV TAG 1.0.0-beta


#######################################################################################################################################################
################################################# Not recommended to edit anything below this line... #################################################
#######################################################################################################################################################


# Setting DEBIAN_FRONTEND variable to noninteractive
ENV DEBIAN_FRONTEND noninteractive

# Adding the official Oracle MySQL APT repositories to install MySQL 5.6 (including the apt-get key)
RUN echo "deb http://repo.mysql.com/apt/debian/ jessie mysql-apt-config" >> /etc/apt/sources.list && \
	echo "deb http://repo.mysql.com/apt/debian/ jessie mysql-5.6" >> /etc/apt/sources.list && \
	echo "deb-src http://repo.mysql.com/apt/debian/ jessie mysql-5.6" >> /etc/apt/sources.list && \
	apt-key adv --keyserver keys.gnupg.net --recv-keys 5072E1F5

# Installing all required packages
RUN apt-get update && \
        apt-get install -y apache2 libapache2-mod-php5 && \
	apt-get install -y mysql-server && \
        apt-get install -y php5 php5-cli php5-curl php5-mysql php5-mcrypt php5-gd php-soap php5-intl php5-common php5-xsl && \
        apt-get install -y git curl sudo

# Adding sudo permissions (no password prompt) for the www-data user
RUN echo "www-data    ALL = NOPASSWD: ALL" >> /etc/sudoers

# Installing composer
RUN sudo curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer && chmod +x /usr/local/bin/composer

# Wiping the /var/www/html/ directory
RUN rm -rf /var/www/* && mkdir /var/www/html && chown -R www-data:www-data /var/www/

# Running all (except for a couple of exceptions that will be addressed using sudo) we want all commands to be run as the www-data user
USER www-data

# Changing our working directory to /var/www/html/
WORKDIR /var/www/html/

# Cloning the Magento 2 project and checking out the required TAG
RUN git clone https://github.com/magento/magento2.git . && git checkout $TAG 

# Setting correct file permissions
RUN find . -type d -exec chmod 700 {} \; && find . -type f -exec chmod 600 {} \; && chmod +x bin/magento

# Running composer to install the required packages
RUN composer install

# Adding custom composer.json file to enable sample data installation
ADD composer.json /var/www/html/

# Fixing ownership of the composer.json file
RUN sudo chown www-data:www-data composer.json

# Fetching the required sample data packages
RUN composer config repositories.magento composer http://packages.magento.com && composer require magento/sample-data:$TAG

# Starting MySQL, creating a DB & installing Magento
RUN sudo service mysql start && mysql -u root -e "create database magento2;" && php bin/magento setup:install --base-url=$MAGE_BASE_URL \
	--backend-frontname=$MAGE_BACKEND_FRONTNAME \
	--db-host=localhost --db-name=magento2 --db-user=root \
	--admin-firstname=$MAGE_ADMIN_FIRSTNAME --admin-lastname=$MAGE_ADMIN_LASTNAME --admin-email=$MAGE_ADMIN_EMAIL \
	--admin-user=$MAGE_ADMIN_USER --admin-password=$MAGE_ADMIN_PASSWORD --language=$MAGE_LANGUAGE \
	--currency=$MAGE_CURRENCY --timezone=$MAGE_TIMEZONE --use-sample-data

# Adding custom vhost to set AllowOverride to All
ADD 000-default.conf /etc/apache2/sites-available/

# Enabling the Apache rewrite module
RUN sudo a2enmod rewrite

# Exposeing port 80
EXPOSE 80

# Starting the Apache & MySQL service on container boot 
CMD sudo service apache2 start && sudo /usr/bin/mysqld_safe
