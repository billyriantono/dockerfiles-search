FROM node:0.12
MAINTAINER Roman Zubatyuk <zubatyuk@gmail.com>

RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
          python-pip python3\ 
    && pip install tentakel \
    && rm -rf /var/lib/apt/lists/* /var/cache/apt/*

RUN    cd /opt \
    && git clone https://bitbucket.org/renambot/sabi.js.git \
    && cd sabi.js \
    && npm install

EXPOSE 9000
WORKDIR /opt/sabi.js
CMD    ["node", "server.js"]
