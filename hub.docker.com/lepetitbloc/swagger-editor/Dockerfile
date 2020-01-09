FROM swaggerapi/swagger-editor

LABEL maintainer='jules@lepetitbloc.net'
EXPOSE 8080
EXPOSE 3000
EXPOSE 3001

RUN apk add --update nodejs
RUN npm -g install browser-sync

COPY ./editor/index.html /usr/share/nginx/html/index.html
COPY ./editor/editor-config.js /usr/share/nginx/html/dist/editor-config.js

COPY spec/swagger.yml /usr/share/nginx/html/data/swagger.yml
VOLUME /usr/share/nginx/html/data/

COPY ./browsersync /data/browsersync
WORKDIR /data/browsersync

COPY ./docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh
ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]
