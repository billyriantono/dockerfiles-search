FROM nginx:1.9

ENV NODE_VERSION 5.10.1

RUN apt-get update \
  && apt-get install --assume-yes --no-install-recommends\
    apt-transport-https \
    bzip2 \
    curl \
    git \
    rlwrap \
    vim \
  && curl https://deb.nodesource.com/node_5.x/pool/main/n/nodejs/nodejs_$NODE_VERSION-1nodesource1~jessie1_amd64.deb > node.deb \
  && dpkg -i node.deb \
  && rm node.deb \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY nginx.conf /etc/nginx/nginx.conf
RUN rm /etc/nginx/conf.d/default.conf

