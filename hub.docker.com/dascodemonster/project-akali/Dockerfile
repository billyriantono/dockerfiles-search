FROM amd64/node:11.5-alpine

WORKDIR /app

COPY ./package.json ./package-lock.json ./

RUN apk add --update \
&& apk add --no-cache --virtual .build-deps git curl python g++ make \
&& npm install \
&& apk del .build-deps \
&& apk add --no-cache ffmpeg

COPY . .

CMD [ "npm", "start" ]
