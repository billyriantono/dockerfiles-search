FROM ubuntu:16.04

RUN apt-get update\
    && apt-get upgrade --no-install-recommends -yqq

RUN apt-get install --no-install-recommends -yqq apt-utils curl gconf-service libasound2 libatk1.0-0 libc6 libcairo2 libcups2 libdbus-1-3 libexpat1 libfontconfig1 libgcc1 libgconf-2-4 libgdk-pixbuf2.0-0 libglib2.0-0 libgtk-3-0 libnspr4 libpango-1.0-0 libpangocairo-1.0-0 libstdc++6 libx11-6 libx11-xcb1 libxcb1 libxcomposite1 libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxss1 libxtst6 ca-certificates fonts-liberation libappindicator1 libnss3 lsb-release xdg-utils wget make build-essential autoconf gcc-multilib g++-multilib lzip python python2.7 libcurl3 git ssh unzip apt-transport-https autotools-dev

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash -

RUN apt-get install -yqq nodejs

RUN npm -g i yarn

RUN yarn global add node-gyp

RUN mkdir -p /root/project

RUN chmod -R 777 /root/project

ENV LANG C.UTF-8
ENV LANGUAGE C.UTF-8
ENV LC_ALL C.UTF-8

CMD tail -f /dev/null