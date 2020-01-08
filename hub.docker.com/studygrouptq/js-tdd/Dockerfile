FROM alpine:3.4

RUN apk update && apk add --no-cache nodejs

RUN mkdir -p /intercom-back

COPY ./package.json /intercom-back/package.json

WORKDIR /intercom-back

RUN npm install

COPY ./src/ /intercom-back/

ENTRYPOINT ["node", "main.js"]