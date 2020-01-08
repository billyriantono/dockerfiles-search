FROM node:8

# trick to get and save chromedriver version
RUN curl -sS chromedriver.storage.googleapis.com/LATEST_RELEASE > /chrome_version

RUN apt-get update \
    && apt-get -y install unzip fonts-liberation libappindicator3-1 libasound2 libatk-bridge2.0-0 libgtk-3-0 libnspr4 libnss3 libx11-xcb1 libxss1 lsb-release xdg-utils \
    && wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \
    && dpkg -i google-chrome-stable_current_amd64.deb \
    && wget -O /tmp/chromedriver.zip http://chromedriver.storage.googleapis.com/$(cat /chrome_version)/chromedriver_linux64.zip \
    && unzip /tmp/chromedriver.zip chromedriver -d /usr/local/bin/ \
    # Ensure that we have latest npm
    && npm install -g npm@latest \
    && npm install -g bower gulp \
    && rm -rf /tmp/* /var/tmp/*
