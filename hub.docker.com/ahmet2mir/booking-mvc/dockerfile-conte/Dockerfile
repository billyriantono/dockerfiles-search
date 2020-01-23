FROM node:alpine

ENV _TEMPORARY_REQUIREMENTS="build-base"
ENV MAGENTO_BUILDPACK_PROVIDE_SECURE_HOST=0

RUN npm install -g yarn
RUN apk add git python

RUN apk --no-cache add --virtual .build-dependencies ${_TEMPORARY_REQUIREMENTS} \
    && git clone https://github.com/magento-research/pwa-studio /app \
    && cd /app  && yarn install \
    && cd /app && cp packages/venia-concept/.env.dist packages/venia-concept/.env && cat packages/venia-concept/.env \
    && apk del .build-dependencies

COPY cmd.sh /cmd.sh

CMD ["sh", "/cmd.sh" ]
