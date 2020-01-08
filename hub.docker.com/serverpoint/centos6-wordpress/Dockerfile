##################################
# Wordpress DockerFile 
##################################
# WP Installation 
##################################

# Set base image for this installation
FROM serverpoint/centos:custom

# Pre-reqs
RUN yum clean all && \
yum -y  update && \
yum -y install httpd mod-rewrite mod-ssl mod-env mysql-server php php-common php-cli php-mysql && \
rm -rf /var/cache/*

# Files that need to be added
ADD mysql-setup.sql /tmp/
ADD wordress.conf /etc/httpd/conf.d/

# Application Install
RUN wget -P /var/www/html/ https://wordpress.org/latest.zip && \
unzip /var/www/html/latest.zip -d /var/www/html/ && \
rm -rf /var/www/html/latest.zip

# RUN MySQL 
RUN service mysqld start && \
mysql < /tmp/mysql-setup.sql && \
rm -rf /tmp/mysql-setup.sql* && \
service mysqld stop 

# Copy & edit the WP-config.php file
RUN cp /var/www/html/wordpress/wp-config-sample.php /var/www/html/wordpress/wp-config.php

RUN sed -ie 's/database_name_here/wordpress/g' /var/www/html/wordpress/wp-config.php && \
sed -ie 's/username_here/wpuser/g' /var/www/html/wordpress/wp-config.php && \
sed -ie 's/password_here/p@ssword/g' /var/www/html/wordpress/wp-config.php

# Set Permission
RUN chown -R apache:apache /var/www/html/wordpress && \
chmod -R 755 /var/www/html/wordpress

# Start service on Boot
RUN echo "service mysqld start" >> ~/.bashrc && \
echo "service httpd start" >> ~/.bashrc
# Expose Ports
EXPOSE 80
