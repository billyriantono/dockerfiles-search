FROM quoaum/alpine-php7

LABEL maintainer="quoaum@gmail.com"

RUN wget https://github.com/getgrav/grav/releases/download/1.6.6/grav-admin-v1.6.6.zip -O /tmp/app.zip

RUN unzip /tmp/app.zip -d /var/www && \
    mv /var/www/grav-admin/* /var/www/ && \
    rm -rf /var/www/grav-admin && \
    rm /tmp/app.zip || true

