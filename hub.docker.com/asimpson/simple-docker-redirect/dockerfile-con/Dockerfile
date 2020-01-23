FROM selenium/node-base:2.45.0
MAINTAINER Selenium <selenium-developers@googlegroups.com>
USER root
#===============
# Google Chrome
#===============
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
&& echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list \
&& apt-get update -qqy \
&& apt-get -qqy install \
google-chrome-stable \
&& rm /etc/apt/sources.list.d/google-chrome.list \
&& rm -rf /var/lib/apt/lists/*
#==================
# Chrome webdriver
#==================
ENV CHROME_DRIVER_VERSION 2.14
RUN wget --no-verbose -O /tmp/chromedriver_linux64.zip http://chromedriver.storage.googleapis.com/$CHROME_DRIVER_VERSION/chromedriver_linux64.zip \
&& rm -rf /opt/selenium/chromedriver \
&& unzip /tmp/chromedriver_linux64.zip -d /opt/selenium \
&& rm /tmp/chromedriver_linux64.zip \
&& mv /opt/selenium/chromedriver /opt/selenium/chromedriver-$CHROME_DRIVER_VERSION \
&& chmod 755 /opt/selenium/chromedriver-$CHROME_DRIVER_VERSION \
&& ln -fs /opt/selenium/chromedriver-$CHROME_DRIVER_VERSION /usr/bin/chromedriver
#========================
# Selenium Configuration
#========================
COPY config.json /opt/selenium/config.json
#=================================
# Chrome Launch Script Modication
#=================================
COPY chrome_launcher.sh /opt/google/chrome/google-chrome
RUN chmod +x /opt/google/chrome/google-chrome
RUN apt-get -qq update
RUN apt-get install xfonts-100dpi xfonts-75dpi xfonts-scalable xfonts-cyrillic
RUN apt-get install dbus-x11
#=========
# Firefox
#=========
RUN apt-get update -qqy \
&& apt-get -qqy --no-install-recommends install \
firefox \
&& rm -rf /var/lib/apt/lists/*
ENV SCREEN_WIDTH 1600
ENV SCREEN_HEIGHT 1000
ENV SCREEN_DEPTH 24
#====================================
# Scripts to run Selenium Standalone
#====================================
COPY entry_point.sh /opt/bin/entry_point.sh
RUN chmod +x /opt/bin/entry_point.sh
USER seluser
EXPOSE 4444
