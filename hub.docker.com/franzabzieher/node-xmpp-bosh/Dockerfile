FROM google/nodejs
MAINTAINER Franz Abzieher <franz@abzieher.net>

WORKDIR /app
COPY node-xmpp-bosh/package.json /app/
RUN npm install
COPY node-xmpp-bosh/. /app

EXPOSE 5280
CMD []
ENTRYPOINT ["/nodejs/bin/npm", "start"]
