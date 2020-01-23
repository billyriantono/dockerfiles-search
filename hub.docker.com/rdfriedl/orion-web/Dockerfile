FROM node:8.9.3-alpine

ARG branch=master
ARG mapbox_api_token="--mapbox_api_token--"
ARG port=80

RUN apk update
RUN apk add curl unzip

RUN curl -L -o orion-web.zip https://github.com/LINKIWI/orion-web/archive/$branch.zip
RUN unzip orion-web.zip
WORKDIR "orion-web-$branch"

RUN npm install
RUN npm install -g node-static

ENV NODE_ENV production
ENV MAPBOX_API_TOKEN $mapbox_api_token
ENV PORT $port

RUN npm run build

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh && chown root:root /entrypoint.sh

EXPOSE $PORT

ENTRYPOINT /entrypoint.sh
