FROM letsbonus/php-dev:5.6

RUN apt-get update && apt-get install -y --no-install-recommends \
    ant \
    cloc \
    openjdk-7-jdk \
    openssh-client \
    unzip \
 && rm -rf /var/lib/apt/lists/* \
 && ln -s /etc/php5/mods-available/xdebug.ini /etc/php5/cli/conf.d/20-xdebug.ini

COPY tooling/* /usr/local/bin/
