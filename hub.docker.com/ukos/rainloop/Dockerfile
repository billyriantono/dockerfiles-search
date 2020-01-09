FROM busybox

RUN mkdir -p /opt/rainloop
RUN mkdir -p /var/www/rainloop

WORKDIR /opt/rainloop
RUN wget -O rainloop-latest.zip http://www.rainloop.net/repository/webmail/rainloop-community-latest.zip
RUN unzip rainloop-latest.zip -d /var/www/rainloop
RUN rm rainloop-latest.zip

WORKDIR /var/www/rainloop
RUN find . -type d -exec chmod 755 {} \;
RUN find . -type f -exec chmod 644 {} \;
RUN chown -R www-data:www-data .
