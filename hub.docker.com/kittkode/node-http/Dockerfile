FROM node:6.9.5-alpine
RUN mkdir -p /usr/src/app/
WORKDIR /usr/src/app
COPY package.json ./package.json
COPY npm-shrinkwrap.json ./npm-shrinkwrap.json
RUN npm install
CMD ["node","node_modules/http-server/bin/http-server","./dest"]
