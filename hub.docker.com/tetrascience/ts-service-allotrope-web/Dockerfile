FROM tetrascience/ts-node:java

WORKDIR /usr/src/app
COPY ./ ./

RUN yarn install --production

EXPOSE 8085

# Run the node server (API + UI)
ENTRYPOINT ["pm2-docker", "start", "processes.docker.api.json"]


