ARG PHP_VERSION=latest
FROM cnsdose/php-apache:$PHP_VERSION

ARG SONAR_SCANNER_VERSION=4.2.0.1873
ARG MYSQL_APT_VERSION=0.8.14-1
ARG CHROME_DRIVER_VERSION=79.0.3945.36

RUN mkdir -p /usr/share/man/man1 \
    && apt-get update && apt-get install -y \
        # common
        libxrender-dev libfontconfig1 libxext6 netcat openjdk-11-jdk python-configparser python3-boto3 python-boto3 valgrind shellcheck \
    && rm -rf /var/lib/apt/lists/*
RUN apt-get update \
    && wget https://dev.mysql.com/get/mysql-apt-config_${MYSQL_APT_VERSION}_all.deb -O mysql-apt-config.deb \
    && DEBIAN_FRONTEND=noninteractive apt-get install -yf ./mysql-apt-config.deb \
    && apt-get update \
    && apt-get install -y mysql-client \
    && rm ./mysql-apt-config.deb \
    && rm -rf /var/lib/apt/lists/*
RUN wget -O /opt/wkhtmltopdf.deb https://downloads.wkhtmltopdf.org/0.12/0.12.5/wkhtmltox_0.12.5-1.stretch_amd64.deb \
    && apt-get update \
    && apt-get install -y -f /opt/wkhtmltopdf.deb \
    && rm /opt/wkhtmltopdf.deb \
    && rm -rf /var/lib/apt/lists/*
# Chrome and Chrome Driver for Laravel Dusk
RUN apt-get update && apt-get install -y \
        xdg-utils libxpm4 libxrender1 libgtk2.0-0 libnss3 libgconf-2-4 xvfb gtk2-engines-pixbuf \
        xfonts-cyrillic xfonts-100dpi xfonts-75dpi xfonts-base xfonts-scalable x11-apps \
    && wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \
    && apt-get install -y -f ./google-chrome-stable_current_amd64.deb \
    && rm google-chrome-stable_current_amd64.deb \
    && wget https://chromedriver.storage.googleapis.com/${CHROME_DRIVER_VERSION}/chromedriver_linux64.zip \
    && unzip chromedriver_linux64.zip \
    && mv chromedriver /usr/local/bin/ \
    && rm chromedriver_linux64.zip \
    && rm -rf /var/lib/apt/lists/*

ADD cnsd-xvfb-run /usr/local/bin/cnsd-xvfb-run
ADD wait-tcp /usr/local/bin/wait-tcp
ADD xdebug_enable /usr/local/bin/xdebug_enable
ADD xdebug_disable /usr/local/bin/xdebug_disable

# PHP DEVELOPMENT INI
RUN cp /usr/local/etc/php/php.ini-development /usr/local/etc/php/php.ini
RUN sed -i -r "s/^memory_limit =.*/memory_limit = -1/" /usr/local/etc/php/php.ini

# PHP DEVELOPMENT EXTENSIONS
RUN CFLAGS="-I/usr/src/php" docker-php-ext-install -j$(nproc) pcntl

# XDEBUG
RUN pecl install xdebug

# SONAR SCANNER
WORKDIR /opt
RUN wget https://dl.bintray.com/sonarsource/SonarQube/org/sonarsource/scanner/cli/sonar-scanner-cli/$SONAR_SCANNER_VERSION/sonar-scanner-cli-$SONAR_SCANNER_VERSION-linux.zip -O sonar-scanner-cli-$SONAR_SCANNER_VERSION-linux.zip && unzip sonar-scanner-cli-$SONAR_SCANNER_VERSION-linux.zip && rm sonar-scanner-cli-$SONAR_SCANNER_VERSION-linux.zip
ENV PATH="/opt/sonar-scanner-$SONAR_SCANNER_VERSION-linux/bin:${PATH}"

WORKDIR /var/www/html
