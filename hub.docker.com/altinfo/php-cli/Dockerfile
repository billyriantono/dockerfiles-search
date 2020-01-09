FROM fedora

LABEL maintainer="Luiz Fernando Pereira <luizfernandopereira@outlook.com.br>"
LABEL company="Alternativa Informática <marcelo@altinfo.com.br>"

RUN dnf install php \
    php-cli \
    php-common \
    php-pdo \
    php-mysqlnd \
    php-pgsql \
    php-mbstring \
    php-xml \
    php-zip \
    php-json \
    php-gd \
    php-soap \
    php-intl \
    php-pear \
    php-pecl-xdebug -y \
    && dnf clean all

ENV TIMEZONE=America/Sao_Paulo
RUN ln -snf /usr/share/zoneinfo/$TIMEZONE /etc/localtime && echo $TIMEZONE > /etc/timezone

COPY php.ini /etc/php.ini
COPY entrypoint.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/entrypoint.sh

ENTRYPOINT [ "/usr/local/bin/entrypoint.sh" ]
CMD ["php", "-a"]