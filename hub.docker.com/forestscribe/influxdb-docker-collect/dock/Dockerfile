FROM python:3.7

LABEL maintainer="FoodLogiQ <technology@foodlogiq.com>"

ENV CHROMEDRIVER_VERSION 2.38

RUN set -xe \
        && wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
        \
        && echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list \
        \
        && apt-get update -y \
        \
        && apt-get install -y \
            unzip \
            google-chrome-stable \
        \
        && apt-get clean \
        \
        && apt-get autoremove

RUN wget -O /tmp/chromedriver.zip "https://chromedriver.storage.googleapis.com/$CHROMEDRIVER_VERSION/chromedriver_linux64.zip" \
        \
        && unzip "/tmp/chromedriver.zip" -d /usr/local/bin \
        \
        && rm "/tmp/chromedriver.zip" 