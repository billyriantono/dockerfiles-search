FROM node:8-alpine

RUN mkdir -p /opt/src/app

WORKDIR /opt
COPY package.json package-lock.json* ./
RUN npm install && npm cache clean --force
ENV PATH /opt/node_modules/.bin:$PATH

WORKDIR /opt/src/app
COPY . /opt/src/app

CMD ["npm", "start"]
