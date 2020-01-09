FROM phusion/baseimage:0.9.15

ENV DEBIAN_FRONTEND noninteractive
ENV COMPOSER_HOME /root/composer

RUN adduser --disabled-password --gecos '' deploy
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y zlib1g zlib1g-dev php5-common git mercurial subversion
RUN apt-get install -y php5-curl php5-gd php5-json php5-mcrypt php5-mysql php5-pgsql php5-readline php5-sqlite sqlite3 mysql-client php5-mysql mcrypt php-pear

RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Display version information
RUN php --version
RUN composer --version

WORKDIR /app

# Set up the command arguments
CMD ["-"]
ENTRYPOINT ["composer", "--ansi"]