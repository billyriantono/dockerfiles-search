FROM alpine:3.8

RUN apk add --no-cache php7 php7-zip php7-intl
RUN apk --update add nodejs nodejs-npm wget curl git php php7-curl php7-openssl php7-json php7-phar php7-dom php7-mbstring yarn openssh-client rsync
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer
RUN curl -LO https://deployer.org/deployer.phar && mv deployer.phar /usr/local/bin/dep && chmod +x /usr/local/bin/dep

