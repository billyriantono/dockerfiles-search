FROM studioibizz/production-php73

# Copied custom configuration for alias and MySQl
COPY conf/vhost.conf /etc/httpd/conf.d/wingzz-vhost.conf
COPY conf/.my.cnf /root/.my.cnf

# install php7 development tools
RUN \
	yum -y install \
		php-devel \
		php-xdebug
COPY ini/50-xdebug.ini /etc/php.d/50-xdebug.ini

# Install mysql client to communicate with other (mysql) containers
RUN yum -y install mysql

# Install Pipeline utilities
RUN pear install PHP_CodeSniffer

# Install Node.js for installing validation tools
RUN yum -y install nodejs

# Install JSHint for checking javascripts
RUN npm install -g eslint

#Install JsonLint to validate json files
RUN npm install -g jsonlint

#Copied scripts for validation
COPY scripts/wingzz.sh /usr/local/bin/wingzz
COPY scripts/wingzz-validate /usr/local/bin/wingzz-validate
RUN ["chmod", "-R", "+x", "/usr/local/bin"]

# Added index to show all local projects
COPY scripts/index.php /var/www/index.php

# Copied script file to run every time
COPY scripts/start.sh /root/scripts/start.sh
RUN ["chmod", "+x", "/root/scripts/start.sh"]

# Set dir projects as working directory
WORKDIR /projects

CMD ["/root/scripts/start.sh"]