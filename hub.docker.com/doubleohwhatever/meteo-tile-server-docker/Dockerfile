##
# idtstudios/meteo-tile-server
#
# Ubuntu 16.04 Xenial Xerus
#FROM ubuntu:xenial
FROM geographica/gdal2:2.3.0

MAINTAINER idtstudios

ENV GIT_REPO https://github.com/user/repo.git


# Load assets
WORKDIR /usr/local/

#Install packages
RUN apt-get update -y && apt-get install -y \
    libboost-all-dev \
    git-core \
    tar \
    unzip \
    sudo \
    wget \
    bzip2 \
    build-essential \
    autoconf \
    libtool \
    libxml2-dev \
    libgeos-dev \
    libgeos++-dev \
    libpq-dev \
    libbz2-dev \
    libproj-dev \
    libprotobuf-c0-dev \
    protobuf-c-compiler \
    libfreetype6-dev \
    libpng12-dev \
    libtiff5-dev \
    libicu-dev \
    libgdal-dev \
    libcairo-dev \
    libcairomm-1.0-dev \
    apache2 \
    apache2-dev \
    libagg-dev \
    liblua5.2-dev \
    ttf-unifont \
    lua5.1 \
    liblua5.1-dev \
    libgeotiff-epsg \
    curl \
    libtool \
    autoconf \
    libtool \
    libxml2-dev \
    libbz2-dev \
    libgeos-dev \
    libgeos++-dev \
    libproj-dev \
    gdal-bin \
    libgdal1-dev \
    libmapnik-dev \
    mapnik-utils  \
    python-mapnik \
    libapache2-mod-php7.0 \
    libapache2-mod-wsgi \
    php \
    php-sqlite3 \
    php-gd \
    php-curl \
    php-mysqli \
    php-xml-parser \
    libapache2-mod-php7.0 \
    php7.0-mbstring \
    libtiff5-dev \
    libpng-dev \
    zlib1g-dev \
    python-pip \
    python-setuptools \
    python-cffi \
    libtiff5 \
    libvips \
    python-qt4 \
    libvips-dev \
    optipng \
    pngquant \
    cron \
    software-properties-common \
    python-software-properties \
    imagemagick \
    php-imagick \
    gfortran \
    checkinstall \
    gcc \
    runit \
    libzmq-dev \
    libmapnik-dev \
    libjpeg-dev

    # Setup Apache
    COPY 000-default.conf /etc/apache2/sites-available/000-default.conf
    RUN echo "ServerName localhost" > /etc/apache2/conf-available/servername.conf && \
     a2enconf servername && a2enmod rewrite

    # Install gdal2mbtiles
    RUN pip install --upgrade pip
    RUN pip install Pillow
    RUN pip install gdal2mbtiles

    # Install tilestache
    RUN easy_install tilestache

    # New php.ini
    RUN rm -Rf /etc/php/7.0/apache2/php.ini
    COPY php.ini /etc/php/7.0/apache2/php.ini

    RUN rm -Rf /var/www
    RUN mkdir /var/www
    RUN mkdir /var/www/wsgi
    RUN chmod +0755 /var/www/wsgi
    RUN chmod +0755 /var/www
    RUN mkdir /var/data
    RUN chmod +0755 /var/data

    # Copy files
    COPY crontab /etc/cron.d/update-cron
    COPY entry.sh /usr/local/entry.sh
    #COPY tilestache.cfg /etc/tilestache.cfg
    #COPY tilestache.wsgi /var/www/wsgi/tilestache.wsgi

    # Conigure permissions
    RUN chmod 0644 /etc/cron.d/update-cron
    RUN chmod +x /usr/local/entry.sh

    #VOLUME /var/www
    VOLUME /var/data
    EXPOSE 80

    # Run the command on container startup
    ENTRYPOINT ["/usr/local/entry.sh"]
    #CMD cron && tail -f /var/log/cron.log
