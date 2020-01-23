FROM ubuntu:bionic
RUN apt-get update && apt-get install git mysql-client software-properties-common -y -qq
RUN ln -sf /usr/share/zoneinfo/Europe/Paris /etc/localtime
RUN apt-get update && apt-get install curl wget php php-cli php7.2 php7.2-common php7.2-curl php7.2-pgsql php7.2-mysql php7.2-intl php7.2-gd php7.2-xml php7.2-opcache php7.2-mbstring php7.2-zip libfontconfig1 fontconfig libxrender-dev libfreetype6 libxrender1 zlib1g-dev xvfb chromium-browser chromium-chromedriver -y -qq
RUN php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php --install-dir=/usr/local/bin --filename=composer && \
    php -r "unlink('composer-setup.php');"
RUN apt-get update && apt-get install unzip -y -qq
ENV PANTHER_CHROME_DRIVER_BINARY="/usr/lib/chromium-browser/chromedriver"
ENV PANTHER_NO_SANDBOX=1
ENV PANTHER_WEB_SERVER_PORT=9800
