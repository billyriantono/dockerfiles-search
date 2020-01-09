FROM alpine:3.7

# Instalando os pacotes necessários
RUN apk --update add --no-cache \
        nginx \
        curl \
        supervisor \
        php7 \
        php7-ctype \
        php7-curl \
        php7-dom \
        php7-fpm \
        php7-json \
        php7-mbstring \
        php7-mcrypt \
        php7-opcache \
        php7-openssl \
        php7-pdo \
        php7-pdo_mysql \
        php7-pdo_pgsql \
        php7-pdo_sqlite \
        php7-phar \
        php7-session \
        php7-tokenizer \
        php7-xml \
        zlib \
        ca-certificates \
        openssl \
        libmemcached \
        rabbitmq-c \
        php7-cgi \
        php7-mbstring \
        php7-mcrypt \
        php7-opcache \
        php7-fileinfo \
        php7-simplexml \
        php7-xmlreader \
        php7-xmlwriter \
        php7-zlib \
        php7-xdebug     

# Limpando o cache das instalações
RUN rm -Rf /var/cache/apk/*

# Instalando composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer

# Configurando o Nginx
# Aqui copiamos nosso arquivo de configuração para dentro do container
COPY nginx.conf /etc/nginx/nginx.conf

# Arquivo de configuração do supervisor
COPY supervisord.conf /etc/supervisord.conf

# Criando o diretório onde ficará nossa aplicação
RUN mkdir -p /app

# Definindo o diretório app como nosso diretório de trabalho
WORKDIR /app

# Dando permissões para a pasta do projeto
RUN chmod -R 755 /app

# Expondo as portas
EXPOSE 80 443

# Finalmente... Iniciando tudo... Ufa...
CMD ["supervisord", "-c", "/etc/supervisord.conf"]