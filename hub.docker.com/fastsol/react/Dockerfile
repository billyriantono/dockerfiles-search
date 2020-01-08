FROM node

ENV NPM_CONFIG_LOGLEVEL warn
ENV APP_ENV production

WORKDIR /frontend
RUN npm install -g http-server

CMD npm install && npm run build && cd build && hs -p 3000

EXPOSE 3000
