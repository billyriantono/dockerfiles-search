FROM node:10

RUN apt-get update && apt-get install -y libnss3 fonts-liberation \
      libappindicator3-1 libasound2 libatk-bridge2.0-0 libatspi2.0-0 \
      libgtk-3-0 libx11-xcb1 libxss1 libxtst6 lsb-release xdg-utils
RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
RUN dpkg -i google-chrome-stable_current_amd64.deb
