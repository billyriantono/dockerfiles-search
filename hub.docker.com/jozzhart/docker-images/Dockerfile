FROM node:6.10
MAINTAINER jozzhart <me@jozzhart.comk>

RUN npm install pm2 -g
RUN npm install phantomjs@1.9.20 -g

EXPOSE 8000 8001 8002

WORKDIR /app

RUN npm install /app/v1 && npm install /app/v2


# Start process.yml
CMD ["pm2-docker", "start", "--auto-exit", "--env", "production", "process.yml"]
