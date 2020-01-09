FROM php:7.3.11-apache-buster
LABEL maintainer="contact@remydamblemont.fr"
RUN apt-get update && apt-get install -y \
    git \
    && rm -rf /var/lib/apt/lists/*
RUN docker-php-ext-install pdo pdo_mysql mbstring hash session
ENV LIMESURVEY_VERSION="3.19.3+191023"
RUN mkdir -p /var/www/html/limesurvey && \
    git clone https://github.com/LimeSurvey/LimeSurvey.git && \
    cd LimeSurvey && git checkout ${LIMESURVEY_VERSION} && cd .. && \
    rm -rf /LimeSurvey/.git && \
    mv LimeSurvey /var/www/html/limesurvey && \
    chown -R www-data:www-data /var/www/html/limesurvey
CMD /usr/sbin/apache2ctl -D FOREGROUND
