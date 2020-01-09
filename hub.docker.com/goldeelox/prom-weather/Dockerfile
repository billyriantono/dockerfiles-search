FROM node:12.4-alpine

WORKDIR /opt/prom-weather
COPY *.js package*.json /opt/prom-weather/

RUN npm install
EXPOSE 3000

CMD [ "npm", "start" ]