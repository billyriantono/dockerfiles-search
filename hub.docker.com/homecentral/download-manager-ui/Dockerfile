FROM node as build

ADD ./src /repo/src
ADD ./*.js /repo/
ADD ./*.json /repo/
ADD ./*.ico /repo/

RUN rm /repo/*lock*.json

WORKDIR /repo

RUN yarn
RUN yarn build

FROM homecentral/base:feature-poc

ADD ./homecentral/ /

COPY --from=build /repo/docs /site/docs
COPY --from=build /repo/node-server.js /site/node-server.js

RUN apk add --no-cache nodejs && \
    chmod +x /entrypoint.sh

WORKDIR /site

VOLUME [ "/config.yml" ]

EXPOSE 8081

ENTRYPOINT [ "/bin/ash", "/entrypoint.sh" ]