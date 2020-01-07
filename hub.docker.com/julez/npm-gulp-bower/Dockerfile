FROM node:7.4.0

RUN npm -g install bower gulp gulp-cli \
  && apt-get update \
  && apt-get install -y git \
  && rm -rf /var/lib/apt/lists/* \
  && echo '{ "allow_root": true }' > /root/.bowerrc
