FROM node:8.14.0-alpine

ARG appdir=/usr/src/app
RUN mkdir -p $appdir
WORKDIR $appdir

WORKDIR $appdir/tmp
COPY package.json $appdir/tmp/.
COPY .npmrc .
RUN npm set progress=false -g
RUN npm install --quiet
RUN ln -s $appdir/tmp/node_modules $appdir/node_modules

WORKDIR $appdir
COPY .env.development .
COPY package.json .
ADD src src/
ADD public public/

CMD [ "npm", "start" ]