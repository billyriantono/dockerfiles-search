FROM waitingsong/node:alpine

LABEL MAINTAINER="waiting"

COPY ./src /app

WORKDIR /app

RUN npm i --prod

VOLUME [ "/app/settings.json" ]

ENTRYPOINT [ "npm", "start" ]

