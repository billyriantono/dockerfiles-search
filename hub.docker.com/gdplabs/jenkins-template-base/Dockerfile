FROM jenkins:1.609.3
MAINTAINER Roy Inganta Ginting <roy.i.ginting@gdplabs.id>

ENV JAVA_OPTS -Dmail.smtp.starttls.enable=true

USER root
COPY php-qa.sh /usr/local/bin/php-qa.sh
RUN apt-get update && apt-get install -y \
    unzip \
    ant \
    jq \
    php5-cli \
    php5-fpm \
    php5-dev \
    php5-mysql \
    php5-mcrypt \
    php5-gd \
    php5-curl \
    php-pear && \
    php-qa.sh && \
    rm -rf /var/lib/apt/lists/*
USER jenkins
