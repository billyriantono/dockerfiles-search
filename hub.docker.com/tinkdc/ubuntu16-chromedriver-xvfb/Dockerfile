FROM ubuntu:16.04

RUN apt-get update && apt-get install -y \
    unzip \
    curl \
    wget \
    openjdk-8-jdk

RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -  \
    && sh -c 'echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list' \
    && apt-get update && apt-get install -y google-chrome-stable \
    xfonts-100dpi xfonts-75dpi xfonts-scalable xfonts-cyrillic xvfb x11-apps


RUN mkdir -p /opt/selenium \
    && curl https://chromedriver.storage.googleapis.com/75.0.3770.90/chromedriver_linux64.zip -o /opt/selenium/chromedriver_linux64.zip \
    && cd /opt/selenium; unzip /opt/selenium/chromedriver_linux64.zip; rm -rf chromedriver_linux64.zip; cp /opt/selenium/chromedriver /; ln -fs /opt/selenium/chromedriver /usr/local/bin/chromedriver;

