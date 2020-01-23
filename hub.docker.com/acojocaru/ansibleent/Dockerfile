FROM node:11.13.0-stretch

RUN echo "installing Debian packages ..." && \
  apt-get update > /dev/null 2>&1 && \
  apt-get install unzip > /dev/null 2>&1 && \
  echo "installing NPM packages ..." && \
  npm config set unsafe-perm true && \
  npm install -g aglio > /dev/null 2>&1 && \
  npm install -g apib2swagger > /dev/null 2>&1 && \
  npm install -g git+https://git@github.com/vlasy/node-swagger-gen.git#aad0408 > /dev/null 2>&1 && \
  npm install -g html-inline > /dev/null 2>&1 && \
  npm install -g @ackee/be-cli > /dev/null 2>&1 && \
  echo "installing Rclone ..." && \
  wget https://github.com/ncw/rclone/releases/download/v1.46/rclone-v1.46-linux-amd64.zip -O rclone.zip > /dev/null 2>&1 && \
  mkdir -p rclone && \
  unzip -j -d rclone rclone.zip > /dev/null 2>&1 && \
  mv rclone/rclone /usr/local/bin && \
  rm -rf rclone rclone.zip
  
