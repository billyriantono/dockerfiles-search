FROM ubuntu:trusty
MAINTAINER BLSQ Dev <tech@bluesquarehub.com>

RUN apt-get update

# Install Apache
RUN apt-get install -y apache2
RUN ls /etc/apt/sources.list.d/

RUN export LANG=C.UTF-8 && \
    apt-get install -y software-properties-common && \
    add-apt-repository -y ppa:nginx/stable && \
    LC_ALL=C.UTF-8 add-apt-repository ppa:ondrej/php -y && \
    apt-get update

# Install PHP
RUN apt-get install -y --force-yes --fix-missing php5.6 php5.6-cli php5.6-readline php5.6-intl php5.6-cli php5.6-json php5.6-mysql php5.6-curl php5.6-dev php5.6-xdebug php5.6-xml php5.6-mcrypt php5.6-mbstring php5.6-gd php5.6-zip libxext6 fontconfig libxrender1 xfonts-base xfonts-75dpi git unzip

# whhtmltppdf package
#ENV WKHTMLTOPDF_DOWNLOAD_URL="https://downloads.wkhtmltopdf.org/0.12/0.12.2.1/wkhtmltox-0.12.2.1_linux-trusty-amd64.deb"
ENV WKHTMLTOPDF_DOWNLOAD_URL="https://s3.eu-central-1.amazonaws.com/blsq-tools/wkhtmltopdf/wkhtmltox-0.12.2.1_linux-trusty-amd64.deb"
ENV WKHTMLTOPDF_DEB="/tmp/wkhtmltopdf.deb"
RUN curl -L --silent -o $WKHTMLTOPDF_DEB $WKHTMLTOPDF_DOWNLOAD_URL && dpkg -i $WKHTMLTOPDF_DEB

# Install composer for PHP dependencies
RUN cd /tmp && curl -sS https://getcomposer.org/installer | php && mv composer.phar /usr/local/bin/composer

# Install expect
RUN apt-get install -y expect