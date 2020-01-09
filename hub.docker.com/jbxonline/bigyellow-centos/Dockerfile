FROM centos:7

# Install yum repo for MariaDB client
COPY MariaDB.repo /etc/yum.repos.d/MariaDB.repo

# Install dependencies and php modules
RUN yum -y install epel-release http://rpms.remirepo.net/enterprise/remi-release-7.rpm yum-utils \
  && curl --silent --location https://rpm.nodesource.com/setup_8.x | bash -

RUN yum update -y && yum --enablerepo=remi --enablerepo=remi-php56 install -y httpd git bc wget mlocate MariaDB-client curl gcc-c++ make nodejs \
  php php-mbstring zip unzip php-zip php-pdo php-pdo_mysql libpng-devel php-gd php-xml php-dom php-bcmath php-gmp php-mcrypt php-soap

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php \
  && chmod +x composer.phar && mv composer.phar /usr/local/bin/composer

# Install grunt cli
RUN npm install -g grunt-cli && npm install -g bower

# Configure apache
COPY bigyellow.conf /etc/httpd/conf.d/bigyellow.conf

# @TODO Configure Xdebug
# RUN echo "memory_limit = 512M" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#   && echo "xdebug.remote_enable = true" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#   && echo "xdebug.remote_connect_back = 0" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#   && echo "xdebug.remote_port = 9000" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#   && echo "xdebug.idekey = PHPSTORM" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#   && echo "xdebug.cli_color = 1" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini \
#   && echo "xdebug.remote_host = docker.for.mac.localhost" >> /usr/local/etc/php/conf.d/docker-php-ext-xdebug.ini

# Add the sqlanywhere libraries and php module
COPY sqlanywhere17 /opt/sqlanywhere17
ENV LD_LIBRARY_PATH="/opt/sqlanywhere17/lib64"
ENV PATH="/opt/sqlanywhere17/bin64:${PATH}"
COPY php-5.6.0_sqlanywhere.so /usr/lib64/php/modules/php-5.6.0_sqlanywhere.so
RUN touch /etc/php.d/30-sqlanywhere.ini \
  && echo "extension=php-5.6.0_sqlanywhere.so" >> /etc/php.d/30-sqlanywhere.ini

# Set the working directory
RUN mkdir -p /var/www/vhosts/bigyellow
WORKDIR /var/www/vhosts/bigyellow

LABEL maintainer="Jon Bowes <jon@jbxonline.net>"

# Serve the site using php's built in web server
COPY entrypoint.sh /usr/local/bin/
RUN chmod u+x /usr/local/bin/entrypoint.sh

CMD bash -c "/usr/local/bin/entrypoint.sh"
