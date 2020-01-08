FROM node:10-alpine

# create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# install dependencies
RUN apk update && apk add samba-client pdftk
COPY package.json package-lock.json /usr/src/app/
RUN npm i --silent

# copy app source
COPY . /usr/src/app

# production environment
ENV NODE_ENV production

# run as non-root
USER node

CMD [ "node", "src/index.js" ]
