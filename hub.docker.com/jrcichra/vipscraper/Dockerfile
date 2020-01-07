FROM vimagick/casperjs
WORKDIR /
RUN apt-get update -y && apt-get install -y git-core curl build-essential openssl libssl-dev \
    && git clone https://github.com/nodejs/node.git \
    && cd node \
    && ./configure \
    && make \
    && make install
ADD package.json /
RUN npm install
ADD vip.js db.js get_active.js vipscraper.sh /
ENV QT_QPA_PLATFORM=offscreen
CMD ["casperjs","/vip.js","${1}", "|", "node db.js"]
