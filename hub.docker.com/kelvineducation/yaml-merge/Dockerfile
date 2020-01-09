FROM node:10-alpine

WORKDIR /app

RUN npm install --global --production @alexlafroscia/yaml-merge
COPY entrypoint.sh /usr/bin/docker-entrypoint.sh

ENTRYPOINT ["/usr/bin/docker-entrypoint.sh", "yaml-merge"]
