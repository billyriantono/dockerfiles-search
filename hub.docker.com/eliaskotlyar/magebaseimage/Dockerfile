FROM eliaskotlyar/magedocker
MAINTAINER elias.kotlyar@gmail.com


RUN export DEBIAN_FRONTEND=noninteractive && \
    apt-get update && \
    apt-get install -q -y \
      mysql-server

COPY scripts/phpmyadminautologin.php /etc/phpmyadmin/conf.d/autologin.php
RUN service mysql start && \
# Create DB:
mysql -u root -e "GRANT ALL ON *.* TO 'database'@'localhost' IDENTIFIED BY 'database'" && \
mysql -u root -e "FLUSH PRIVILEGES"


