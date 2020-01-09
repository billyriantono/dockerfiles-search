FROM ubuntu:precise
MAINTAINER A-Marwan <amamou.marwan@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y git bzip2 wget make php-pear php5-dev php5-xdebug imagemagick php5-tidy libsqlite3-0 libsqlite3-dev php5-sqlite php5-intl php5-curl gvfs-bin shared-mime-info xpdf poppler-utils ghostscript subversion lpr libart-2.0-2 zlib1g-dev libfreetype6-dev libjpeg62-dev libgif4 g++ apache2 mysql-client php5-mysql libapache2-mod-php5 php5-gd php5-ldap php5-odbc git-core php5-intl php5-imagick libimage-exiftool-perl libgtk2.0-dev xvfb libc6-i386 libglib2.0-0:i386 ia32-libs sudo

RUN pear install pear/OLE-1.0.0RC2 && \
    pear install Spreadsheet_Excel_Writer-0.9.3

WORKDIR /tmp/builds

RUN wget https://wkhtmltopdf.googlecode.com/files/wkhtmltoimage-0.11.0_rc1-static-amd64.tar.bz2 && \
    tar -xf wkhtmltoimage-0.11.0_rc1-static-amd64.tar.bz2 && \
    cp wkhtmltoimage-amd64 /usr/bin/wkhtmltoimage

ADD swftools-0.9.1.tar.gz ttf2pt1-3.4.4.tgz /tmp/builds/

WORKDIR /tmp/builds/swftools-0.9.1

RUN ./configure && \
    make && \
    make install && \
    cd ..

WORKDIR /tmp/builds/ttf2pt1-3.4.4

RUN make t1asm ttf2pt1 docs mans && \
    make install

RUN rm -rf /etc/php5/cli/php.ini && \
    ln -s /etc/php5/apache2/php.ini /etc/php5/cli/php.ini

RUN echo "date.timezone= Europe/Paris" >>  /etc/php5/apache2/php.ini && \
    echo "phar.readonly = Off" >> /etc/php5/apache2/php.ini && \
    echo "html_errors = On" >> /etc/php5/apache2/php.ini && \
    echo "display_errors = On" >> /etc/php5/apache2/php.ini && \
    echo "error_reporting = E_ALL"  >> /etc/php5/apache2/php.ini && \
    echo "display_startup_errors = On" >> /etc/php5/apache2/php.ini && \
    echo "xdebug.max_nesting_level = 250" >>  /etc/php5/apache2/php.ini && \
    echo "xdebug.var_display_max_depth = 10" >> /etc/php5/apache2/php.ini

RUN sed -i -e "s/^max_execution_time\s*=.*/max_execution_time = 300/" \
-e "s/^post_max_size\s*=.*/post_max_size = 4G/" \
-e "s/^upload_max_filesize\s*=.*/upload_max_filesize = 4G\nupload_max_size = 4G/" \
-e "s/^memory_limit\s*=.*/memory_limit = 4G/" /etc/php5/apache2/php.ini

RUN cd /tmp && \
    php -r "readfile('https://getcomposer.org/installer');" | php && \
    mv composer.phar /usr/local/bin/composer

WORKDIR /

RUN rm -rf /tmp/builds

RUN a2enmod rewrite && \
    service apache2 restart

ADD default /etc/apache2/sites-available/

ADD run.sh /run.sh
RUN chmod 755 /*.sh

EXPOSE 80
EXPOSE 443

WORKDIR /DNA

CMD ["/run.sh"]


RUN apt-get install nano

RUN apt-get autoremove && \
    apt-get autoclean && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

