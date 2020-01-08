FROM node:8

RUN apt-get update && apt-get install -y fonts-liberation libappindicator3-1 libasound2 libatk-bridge2.0-0 libatspi2.0-0 libgtk-3-0 libnspr4 libnss3 libx11-xcb1 libxss1 libxtst6 lsb-release xdg-utils

RUN mkdir /opt/chrome
ADD ./deb/google-chrome-stable_73.0.3683.86-1_amd64.deb /opt/chrome/
RUN dpkg -i /opt/chrome/google-chrome-stable_73.0.3683.86-1_amd64.deb
RUN rm /opt/chrome/google-chrome-stable_73.0.3683.86-1_amd64.deb
ADD ./bin/chromedriver /opt/chrome/
RUN mkdir /opt/selenium
ADD ./jar/selenium-server-standalone.jar /opt/selenium/
