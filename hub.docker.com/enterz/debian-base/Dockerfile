FROM debian:stretch

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -y update \
&& apt-get -y install \
curl \
sudo \
wget \
gnupg \
default-jre \
software-properties-common \
&& java -version

# Nodejs 9 with npm install and Protractor , WebDriver Manager
# https://github.com/nodesource/distributions#installation-instructions
RUN curl -sL https://deb.nodesource.com/setup_9.x | sudo -E bash -
RUN apt-get update -y \
&& apt-get -y install nodejs \
&& node -v && npm --version \
&& npm install -g protractor \
&& protractor --version \
&& webdriver-manager update

RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add -
RUN echo 'deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main' | sudo tee /etc/apt/sources.list.d/google-chrome.list 

RUN apt-get update -y \
&& apt-get install -y libxpm4 libxrender1 libgtk2.0-0 libnss3 libgconf-2-4 \
google-chrome-stable \
xvfb gtk2-engines-pixbuf \
xfonts-cyrillic xfonts-100dpi xfonts-75dpi xfonts-base xfonts-scalable \
imagemagick x11-apps dbus-x11

RUN xvfb-run -a --server-args="-screen 0 2880x1800x24" &

# Set the working directory
WORKDIR /protractor/

COPY conf.js /protractor/conf.js
COPY spec.js /protractor/spec.js
COPY package.json /protractor/package.json

RUN webdriver-manager start --standalone &
RUN npm test && ls -la