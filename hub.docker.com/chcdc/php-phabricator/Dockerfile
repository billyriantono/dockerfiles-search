FROM ubuntu
LABEL maintainer="carlos@chcdc.com.br"
ARG DEBIAN_FRONTEND=noninteractive

RUN apt update -qq && \
    apt-get install -y --no-install-recommends \
    apache2 git apache2 php-xml \ 
    libapache2-mod-php php tree \
    php-mysql subversion \
    python3-pip php-gd php-curl \ 
    php-apcu php-cli php-ldap \
    ca-certificates procps locales \
    php-json php-mbstring \ 
    php-zip language-pack-en-base && \
    rm -rf /var/lib/apt/lists/* && \
    a2enmod rewrite && \
    apt-get autoremove -y && \
    apt-get autoclean && \
    rm /etc/apache2/sites-enabled/000-default.conf && \
    pip3 install Pygments && \
    locale-gen en_GB.UTF-8 && \
    locale-gen en_US.UTF-8

WORKDIR /var/www/

# File Uploads
RUN { \
        echo 'post_max_size=32M'; \
        echo 'upload_max_filesize=32M'; \
    } > /etc/php/7.2/apache2/conf.d/uploads.ini

RUN { \
        echo 'date.timezone=America/Sao_Paulo'; \
        echo 'opcache.memory_consumption=128'; \
        echo 'opcache.interned_strings_buffer=8'; \
        echo 'opcache.max_accelerated_files=4000'; \
        echo 'opcache.revalidate_freq=60'; \
        echo 'opcache.fast_shutdown=1'; \
        # From Phabricator
        echo 'opcache.validate_timestamps=0'; \
    } > /etc/php/7.2/apache2/conf.d/php.ini

# Repository Folder.
RUN mkdir /var/repo \
    && chown www-data:www-data /var/repo 

# Git clone Phabricator
RUN git clone https://github.com/phacility/libphutil.git && \
    cd libphutil && git pull --rebase && cd
RUN git clone https://github.com/phacility/arcanist.git && \
    cd arcanist && git pull --rebase && cd
RUN git clone https://github.com/phacility/phabricator.git && \
    cd phabricator && git pull --rebase && cd

COPY phabricator.conf /etc/apache2/sites-enabled/
COPY run.sh /var/www/
ENV PATH "$PATH:/var/www/phabricator/bin:/var/www/arcanist/bin"
ENV LC_ALL=C

# Configure Phabricator
RUN ln -s /usr/lib/git-core/git-http-backend /usr/bin/git-http-backend
RUN config set storage.mysql-engine.max-size 8388608 
RUN config set pygments.enabled true

CMD /var/www/run.sh
