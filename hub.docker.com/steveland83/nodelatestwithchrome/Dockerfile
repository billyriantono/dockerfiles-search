FROM node:latest
# update apt-get
RUN apt-get update; apt-get clean
# Install xvfb.
RUN apt-get install -y xvfb
# Install wget.
RUN apt-get install -y wget
# Install ncftp.
RUN apt-get install -y ncftp
# Set the Chrome repo.
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list
# Install Chrome.
RUN apt-get update && apt-get -y install google-chrome-stable

ENV CHROME_BIN /usr/bin/google-chrome
