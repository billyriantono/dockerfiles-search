FROM node:7.10.0

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6 \
  && echo "deb http://repo.mongodb.org/apt/debian jessie/mongodb-org/3.4 main" | tee /etc/apt/sources.list.d/mongodb-org-3.4.list \
  && apt-get update \
  && apt-get dist-upgrade -y \
  && apt-get install -y mongodb-org redis-server \
  && apt-get clean -y \
  && rm -rf /var/lib/apt/lists/* \
  && rm -rf /var/cache/apt/*

COPY package.json /tmp

RUN cd /tmp \
  && yarn --version \
  && yarn config set registry https://registry.npmjs.org/ \
  && yarn --pure-lockfile \
  && rm -rf /tmp/package.json \
  && rm -rf /tmp/node_modules
