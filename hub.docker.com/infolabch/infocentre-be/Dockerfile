FROM node:10

WORKDIR /data

WORKDIR /infocentre-backend

COPY . /infocentre-backend/

RUN npm install pm2 -g
RUN npm install

CMD ["pm2-runtime", "/config/infocentre.json"]
