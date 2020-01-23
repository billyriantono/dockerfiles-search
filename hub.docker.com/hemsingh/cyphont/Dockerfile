FROM node:6

MAINTAINER Andi N. Dirgantara <andi.nugroho@salestock.id>

# install host utilities
RUN apt-get update
RUN apt-get install ocaml libelf-dev -y
RUN curl -o- -L https://yarnpkg.com/install.sh | bash

# install PM2 and update NPM
RUN yarn global add pm2

# create app directory
RUN mkdir -p /app
WORKDIR /app

# copy project and run installation
COPY . /app
RUN rm -rf /app/node_modules
RUN yarn install
RUN yarn flow
RUN yarn test
RUN yarn build

# re-install in production mode
RUN rm -rf /app/node_modules
RUN yarn install --production

ENV NODE_PATH=./lib

CMD [ "pm2", "start", "--no-daemon", "index.js"]
EXPOSE 80
