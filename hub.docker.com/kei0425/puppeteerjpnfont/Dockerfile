FROM alekzonder/puppeteer:latest
# Japanese font
RUN echo 'deb http://ftp.jp.debian.org/debian jessie-backports main' >> /etc/apt/sources.list
RUN apt-get update && apt-get -y install fonts-ipafont
WORKDIR /app

