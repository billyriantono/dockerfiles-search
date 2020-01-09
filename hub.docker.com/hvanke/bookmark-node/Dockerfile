FROM node:8.12.0-alpine

WORKDIR /app

COPY . /app
RUN apk add --no-cache --virtual .gyp \
        python \
        make \
        g++ \ 
        && yarn --pure-lockfile \
        && apk del .gyp

EXPOSE 3001

CMD ["npm", "run", "prod"]
