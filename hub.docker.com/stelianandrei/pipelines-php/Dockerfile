FROM ubuntu:18.04

# run in non interactive mode
ARG DEBIAN_FRONTEND=noninteractive

# update packages and requirements
RUN apt-get -qq update && apt-get -qq upgrade -y
RUN apt-get -qq install -y software-properties-common curl openssh-client rsync zip sqlite3

# install NodeJS
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
RUN apt-get install -y nodejs

# add the PHP repository
RUN add-apt-repository ppa:ondrej/php -y > /dev/null

# install PHP and modules
RUN apt-get -qq install -y php7.3-cli php7.3-mbstring php7.3-json php7.3-curl php7.3-xml php7.3-bcmath php7.3-mysql php7.3-gd php7.3-sqlite3 php7.3-zip php7.3-xdebug

# install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# install AWS CLI
RUN apt-get -qq install -y awscli
