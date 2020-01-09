FROM fedora:latest

LABEL maitainer="Luiz Fernando Pereira <luizfernandopereira@outlook.com.br>" \
      company="Alternativa Informática"

RUN dnf -y install \
    git \
    composer \
    php \
    php-common \
    php-cli \
    php-mbstring \
    php-xml \
    php-pgsql \
    php-mysqlnd \
    php-pdo \
    php-gd \
    php-soap \
    php-intl \
    php-pear \
    php-interbase \
    php-zip \
    php-json \
    php-ldap \
    php-pecl-mcrypt \
    php-pecl-ssh2 \
    openssl \
    openssh \
    php-snmp

ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /sbin/tini
RUN chmod +x /sbin/tini

RUN mkdir  /.composer
RUN chmod 777 /.composer

COPY entrypoint.sh /entrypoint.sh

RUN chmod +x /entrypoint.sh

WORKDIR /app

ENTRYPOINT ["/bin/sh", "/entrypoint.sh"]

CMD ["composer"]