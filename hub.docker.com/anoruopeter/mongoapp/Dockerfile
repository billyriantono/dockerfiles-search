FROM keymetrics/pm2:latest-alpine


COPY . /source 

ENV NPM_CONFIG_LOGLEVEL warn

ENV TZ Europe/Berlin


WORKDIR /source
RUN npm install --production


CMD [ "pm2-runtime", "start", "/source/pm2.json" ]