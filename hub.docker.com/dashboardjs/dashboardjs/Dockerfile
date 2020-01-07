FROM node:4-slim

RUN mkdir -p /dashboardjs
WORKDIR /dashboardjs

ENV PROVIDER_DIR=/provider \
    PROVIDER_CONFIG=/config/provider \
    SOURCE_CONFIG=/config/source

COPY package.json /dashboardjs/
RUN npm install --production
COPY server.js /dashboardjs/

CMD [ "npm", "start" ]
