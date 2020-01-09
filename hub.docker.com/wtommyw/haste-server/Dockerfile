FROM node

ADD . /opt/haste
WORKDIR /opt/haste

RUN npm install

expose 7777

cmd ["npm", "start"]
