FROM node:8.7.0-alpine

RUN mkdir -p /srv/app/avatar-client
WORKDIR /srv/app/avatar-client

COPY package.json /srv/app/avatar-client
COPY package-lock.json /srv/app/avatar-client

RUN npm install

COPY . /srv/app/avatar-client

CMD ["npm", "start"]