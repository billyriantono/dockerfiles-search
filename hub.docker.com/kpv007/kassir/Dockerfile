FROM node:alpine

WORKDIR /opt/kassir
ADD package.json package.json
ADD package-lock.json /tmp/package-lock.json
RUN npm install
ADD . /opt/kassir

ENTRYPOINT ["npm", "run", "start"]