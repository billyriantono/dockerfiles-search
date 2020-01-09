FROM node:7.4.0-slim

MAINTAINER Ole G. Nedrebø

RUN apt-get update -y && \
    apt-get install -y php5-cli curl php5-curl git php5-mcrypt php5-gd && \
    curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN npm set progress=false && \
    npm install -g --progress=false yarn

RUN npm install -g --progress=false webpack@2.2.0-rc.3

RUN npm install -g --progress=false gulp-cli
