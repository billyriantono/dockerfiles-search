FROM node:10-alpine

ENV VS_ENV prod

WORKDIR /var/www

COPY package.json ./
COPY yarn.lock ./

RUN apk add --no-cache --virtual .build-deps ca-certificates wget git \
  && yarn install --no-cache \
  && apk del .build-deps

COPY vue-storefront.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/vue-storefront.sh

CMD ["vue-storefront.sh"]
