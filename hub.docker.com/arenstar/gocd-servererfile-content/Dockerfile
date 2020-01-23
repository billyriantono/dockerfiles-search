# Ubuntu Xenial = 16.04
FROM ubuntu:xenial

LABEL vendor="Arc'teryx Equipment"
LABEL maintainer="Web Team"
LABEL com.arcteryx.version="0.1.7"
LABEL com.arcteryx.release-date="2018-12-04"

# Install build software
RUN apt-get update && apt-get install -y \
  curl \
  git \
  python-pip \
  nginx \
  gconf-service libasound2 libatk1.0-0 libc6 libcairo2 libcups2 libdbus-1-3 libexpat1 libfontconfig1 libgcc1 libgconf-2-4 libgdk-pixbuf2.0-0 libglib2.0-0 libgtk-3-0 libnspr4 libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libx11-6 libx11-xcb1 libxcb1 libxcomposite1 libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxss1 libxtst6 ca-certificates fonts-liberation libappindicator1 libnss3 lsb-release xdg-utils wget

# the last line is all the dependencies for headless chrome, from
# https://github.com/GoogleChrome/puppeteer/blob/master/docs/troubleshooting.md#chrome-headless-doesnt-launch

# Install NodeJS v8
# https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions
RUN curl -sL https://deb.nodesource.com/setup_8.x | bash -
RUN apt-get update && apt-get install -y nodejs

RUN pip install -U awscli

COPY nginx.conf /etc/nginx/sites-available/
COPY SSL/cert.crt /etc/nginx/ssl/
COPY SSL/cert.key /etc/nginx/ssl/

RUN ln -s /etc/nginx/sites-available/nginx.conf /etc/nginx/sites-enabled/webscripts
