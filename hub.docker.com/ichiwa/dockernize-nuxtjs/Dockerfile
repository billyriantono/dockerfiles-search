FROM keymetrics/pm2:8-alpine

COPY . /src
WORKDIR /src

ENV NPM_CONFIG_LOGLEVEL warn
ENV HOST 0.0.0.0
ENV PORT 8080
RUN npm install
RUN npm run build

CMD [ "pm2-docker", "start", "npm", "--", "start" ]
