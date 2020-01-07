FROM debian:stretch-slim
MAINTAINER Galileo Martinez "gmartinez@tacitknowledge.com"
ENV REFRESHED_AT 2018-Aug-16

ENV CHROMEDRIVER_VERSION 2.41
ENV GECKODRIVER_VERSION 0.21.0
ENV FIREFOXBROWSER_VERSION 60.0.1
ENV DEPS wget curl unzip

RUN apt-get update \
 && apt-get install -y $DEPS gcc python python-pip libdbus-glib-1-dev libgtk2.0-0\
 ## Install Chrome
 && wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
 && echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list \
 && apt-get update && apt-get install -y google-chrome-stable \
 ## Install Firefox
 && wget https://ftp.mozilla.org/pub/firefox/releases/$FIREFOXBROWSER_VERSION/linux-x86_64/en-US/firefox-$FIREFOXBROWSER_VERSION.tar.bz2 \
 && tar -xjf "firefox-$FIREFOXBROWSER_VERSION.tar.bz2" \
 && mv firefox /opt/firefox \
 && rm "firefox-$FIREFOXBROWSER_VERSION.tar.bz2" \
 ## Move Binaries, place headless script (Firefox)
 && echo $'#!/bin/bash\n\
firefox-browser -headless $@ &\n\
ff=$!\n\
wait $ff' > /usr/bin/headless-firefox \
 && ln -s /opt/firefox/firefox /usr/bin/firefox-browser \
 && ln -s /usr/bin/headless-firefox /usr/bin/firefox \
 && chmod a+x /usr/bin/headless-firefox \
 ## Move Binaries, place headless script (Chrome)
 && echo $'#!/bin/bash\n\
chrome --headless --disable-gpu --no-sandbox $@ &\n\
chrome=$!\n\
wait $chrome' > /usr/bin/headless-chrome \
 && mv /opt/google/chrome/google-chrome /opt/google/chrome/google-chrome-browser \
 && rm /usr/bin/google-chrome-stable \
 && rm /usr/bin/google-chrome \
 && ln -s /opt/google/chrome/google-chrome-browser /usr/bin/chrome \
 && ln -s /usr/bin/headless-chrome /usr/bin/google-chrome \
 && chmod a+x /usr/bin/headless-chrome \
 ## Download Browser Drivers
 && curl -SLO "https://chromedriver.storage.googleapis.com/$CHROMEDRIVER_VERSION/chromedriver_linux64.zip" \
 && unzip "chromedriver_linux64.zip" -d /usr/local/bin \
 && rm "chromedriver_linux64.zip" \
 && curl -SLO "https://github.com/mozilla/geckodriver/releases/download/v$GECKODRIVER_VERSION/geckodriver-v$GECKODRIVER_VERSION-linux64.tar.gz" \
 && tar zxvf "geckodriver-v$GECKODRIVER_VERSION-linux64.tar.gz" -C /usr/local/bin \
 && rm "geckodriver-v$GECKODRIVER_VERSION-linux64.tar.gz" \
 ## Install robotFramework and deps
 && pip install robotframework robotframework-selenium2library robotframework-faker robotframework-pabot
