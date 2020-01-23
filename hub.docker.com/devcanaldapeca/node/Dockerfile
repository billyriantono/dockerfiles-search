FROM node:9.5.0-alpine

RUN mkdir /src
RUN npm install pm2 -g
WORKDIR /src

# Setup startup script
COPY docker-entrypoint.sh /docker-entrypoint.sh
RUN chmod +x /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]
