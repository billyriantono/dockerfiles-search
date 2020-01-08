FROM node:6.9.5-slim

ENV PORT 8080

RUN mkdir -p /app/logs

WORKDIR /app/
RUN npm install -g pushstate-server
ADD package.json /app/
RUN npm install

ADD . /app/
RUN npm run build

EXPOSE 8080

ENTRYPOINT ["/app/docker-entrypoint.sh"]
