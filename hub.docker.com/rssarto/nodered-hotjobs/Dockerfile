FROM nodered/node-red-docker

COPY ./package.json /data/package.json
COPY ./settings.js /data/settings.js
COPY ./flows.json /data/flows.json
RUN cd /data && npm install