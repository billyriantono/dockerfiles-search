FROM       node:7-slim
MAINTAINER Ilya Nekhozhin <nekhozhin@live.com>

COPY . /
WORKDIR /

RUN apt-get update && apt-get install -y libpng12-0 nano
RUN npm install -g yarn && npm install babel-core babel-loader --save-dev && npm rebuild node-sass && yarn install
RUN ln -sf /node_modules/.bin/gulp /usr/bin/gulp
USER node

CMD ["gulp"]
