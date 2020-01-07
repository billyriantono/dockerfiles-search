FROM node:10

RUN apt-get update
RUN apt-get install -yy wget curl gnupg zip firefox-esr

RUN npm install -g npm@latest

RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - && \
  echo "deb http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google.list && \
  apt-get update && \
  apt-get install -y google-chrome-stable xvfb

RUN npm -v
RUN rm -rf /var/lib/apt/lists/*
