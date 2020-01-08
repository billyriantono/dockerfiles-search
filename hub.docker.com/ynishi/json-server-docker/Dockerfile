FROM node:10.6.0-alpine

RUN set eux; \
  yarn global add json-server@0.14.0 \
  && json-server --version

RUN set eux; \
  mkdir /data \
  && touch /data/db.json
WORKDIR /data

EXPOSE 3000
CMD ["json-server","--host","0.0.0.0","db.json"]
