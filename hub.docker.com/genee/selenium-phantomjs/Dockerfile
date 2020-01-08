FROM debian:7.6
MAINTAINER jia.huang@geneegroup.com

ENV DEBIAN_FRONTEND noninteractive

# Install cURL
RUN apt-get update && apt-get install -y curl apt-utils

# Install NodeJS
RUN (curl -sL https://deb.nodesource.com/setup | bash -) && \
    apt-get install -y nodejs && npm install -g phantomjs

ENV WEBDRIVER 172.17.42.1:5555
ENV HUB http://172.17.42.1:4444

EXPOSE 5555

CMD phantomjs --webdriver=$WEBDRIVER --webdriver-selenium-grid-hub=$HUB