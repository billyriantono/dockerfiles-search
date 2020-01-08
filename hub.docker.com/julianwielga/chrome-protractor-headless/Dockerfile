FROM node:slim
WORKDIR /tmp

RUN echo "deb http://dl.google.com/linux/chrome/deb/ stable main" | tee -a /etc/apt/sources.list
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -

RUN apt-get update -y
RUN apt-get -y install libxpm4 libxrender1 libgtk2.0-0 libnss3 libgconf-2-4 openjdk-7-jre-headless
RUN apt-get -y install xvfb gtk2-engines-pixbuf x11vnc
RUN apt-get -y install imagemagick x11-apps
RUN apt-get -y install xfonts-cyrillic xfonts-100dpi xfonts-75dpi xfonts-base xfonts-scalable
RUN apt-get -y install google-chrome-stable

RUN npm install protractor -g
RUN npm install -g mocha jasmine coffee-script
RUN webdriver-manager update

RUN mkdir /project
ADD protractor.sh /entry.sh

# Fix for the issue with Selenium, as described here:
# https://github.com/SeleniumHQ/docker-selenium/issues/87
ENV DBUS_SESSION_BUS_ADDRESS=/dev/null
WORKDIR /project

# EXPOSE 4444 5999
ENTRYPOINT ["/entry.sh"]
