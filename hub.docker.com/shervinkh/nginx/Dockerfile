FROM shervinkh/my-archlinux
MAINTAINER "Shervin Khastoo" <shervinkh145@gmail.com>
RUN /update.sh && \
    pacman -S --noconfirm nginx-mainline php-fpm && \
    sed --in-place 's/;date.timezone =/date.timezone = "Iran"/' /etc/php/php.ini && \
    mkdir -p /www && \
    /cleanup.sh
COPY configs /etc/
COPY scripts /scripts/
EXPOSE 80 9001
