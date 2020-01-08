# Use the node image
FROM node:alpine

RUN mkdir -p /usr/quickstart

ADD . /usr/quickstart

WORKDIR /usr/quickstart

RUN npm install

EXPOSE 3000 3001

RUN ls

CMD ["npm", "start"]
