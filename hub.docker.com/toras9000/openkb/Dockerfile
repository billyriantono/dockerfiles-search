FROM node:10-slim

ARG OPENKB_VER=master

WORKDIR /openkb

# install
RUN apt-get update \
 && apt-get install -y git python gcc g++ make \
 && cd /openkb \
 && git clone https://github.com/mrvautin/openKB.git -b ${OPENKB_VER} --depth 1 . \
 && cp config/config.json config.org.json \
 && rm -rf .git \
 && npm install \
 && apt-get purge -y git python gcc g++ make \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

# for minify
RUN npm run uglify
ENV NODE_ENV="production node app.js"

# copy assets
COPY ./assets/startup.sh /openkb/startup.sh

EXPOSE 4444

CMD ["bash", "/openkb/startup.sh"]
