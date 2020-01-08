FROM alpine:latest

RUN apk --no-cache add php7 php7-fpm php7-json php7-zlib php7-xml php7-phar php7-iconv php7-mcrypt curl php7-curl php7-openssl php7-gd php7-dom  php7-ctype php7-pdo php7-pdo_mysql php7-zip php7-xml php7-simplexml php7-xmlreader php7-mbstring php7-apcu php7-xmlrpc php7-memcached php7-dom php7-common php7-fileinfo php7-tokenizer php7-xmlwriter zip python3 wget && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer && wget -O /usr/local/bin/phpunit https://phar.phpunit.de/phpunit-7.phar && chmod +x /usr/local/bin/phpunit && wget https://bootstrap.pypa.io/get-pip.py && python3 get-pip.py && pip install boto3==1.3.0

