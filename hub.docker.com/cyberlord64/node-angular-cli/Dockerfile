# Base Image
FROM node:12
RUN apt-get update -y \
    && apt-get upgrade -y \
    && apt-get install libxss1 libappindicator1 libindicator7 fonts-liberation libappindicator3-1 libasound2 libatk-bridge2.0-0 libatspi2.0-0 libgtk-3-0 libnspr4 libnss3 libx11-xcb1 libxtst6 lsb-release xdg-utils -y \
    && wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \
    && dpkg -i google-chrome*.deb \
    && apt-get install -f \
