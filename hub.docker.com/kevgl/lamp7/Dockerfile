FROM    ubuntu:xenial

MAINTAINER Kevin Gliewe "kevingliewe@gmail.com"

ENV     DEBIAN_FRONTEND noninteractive

ENV     UID 1000

ENV     MYSQL_USER admin
ENV     MYSQL_PASSWORD admin

ENV     MYSQL_DATABASE app

EXPOSE  80

# Install Misc.
RUN     apt-get --yes update && \
        apt-get --yes upgrade && \
        apt-get --yes install sudo nano curl git xclip apt-transport-https && \
        curl https://getmic.ro | bash && \ 
        mv ./micro /bin

# Install PowerShell
RUN     curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - && \
        curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list | tee /etc/apt/sources.list.d/microsoft.list && \
        apt-get update && \
        apt-get install -y powershell && \
        pwsh -c Install-Package psake -Force && \
        chmod -R 777 /root

ADD    ./scripts/mysql.cnf  /etc/mysql/my.cnf

# Install apache2 php7 and mysql
RUN     apt-get --yes install mysql-server && \
        apt-get --yes install apache2 && \
        apt-get --yes install php php-cli php-mysql php-imagick php-mcrypt php-pear php-dev php-curl php-zip php-intl php-soap libapache2-mod-php composer && \
        a2enmod rewrite && \
        /etc/init.d/mysql restart && \
        /etc/init.d/apache2 restart

# Intall and configure PhpMyAdmin
RUN     apt-get --yes install phpmyadmin && \
        echo 'Include /etc/phpmyadmin/apache.conf' >> /etc/apache2/apache2.conf

# Add apache Configuration
ADD     scripts/000-default.conf /etc/apache2/sites-enabled/000-default.conf

# Import database and setting up user for for PhpMyAdmin
RUN     sed -i "s/\$dbuser/'phpmyadmin'/g" /etc/phpmyadmin/config.inc.php && \
        sed -i "s/\$dbpass/'xbEDb39XsnOod331ca'/g" /etc/phpmyadmin/config.inc.php && \
        sed -i 's/pma_bookmark/pma__bookmark/g' /etc/phpmyadmin/config.inc.php && \
        sed -i 's/pma_relation/pma__relation/g' /etc/phpmyadmin/config.inc.php && \
        sed -i 's/pma_table_info/pma__table_info/g' /etc/phpmyadmin/config.inc.php && \
        sed -i 's/pma_table_coords/pma__table_coords/g' /etc/phpmyadmin/config.inc.php && \
        sed -i 's/pma_pdf_pages/pma_pdf__pages/g' /etc/phpmyadmin/config.inc.php && \
        sed -i 's/pma_column_info/pma__column_info/g' /etc/phpmyadmin/config.inc.php && \
        sed -i 's/pma_history/pma__history/g' /etc/phpmyadmin/config.inc.php && \
        sed -i 's/pma_table_uiprefs/pma__table_uiprefs/g' /etc/phpmyadmin/config.inc.php && \
        sed -i 's/pma_designer_coords/pma__designer_coords/g' /etc/phpmyadmin/config.inc.php && \
        sed -i 's/pma_tracking/pma__tracking/g' /etc/phpmyadmin/config.inc.php && \
        sed -i 's/pma_userconfig/pma__userconfig/g' /etc/phpmyadmin/config.inc.php && \
        sed -i 's/pma_recent/pma__recent/g' /etc/phpmyadmin/config.inc.php

RUN     /etc/init.d/mysql stop && \
        mkdir /var/lib/mysql.back && \
        mv /var/lib/mysql/* /var/lib/mysql.back

# Load in all script files.
ADD    ./scripts/start /start

# Fix the permissions
RUN    chmod +x /start

VOLUME /var/lib/mysql
VOLUME /var/www/html

# /start runs it.
CMD    ["/start"]