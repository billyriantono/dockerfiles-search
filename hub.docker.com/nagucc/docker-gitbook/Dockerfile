FROM node:7.7.0-alpine
RUN npm install -g gitbook-cli
RUN npm -g install web-server-cli
RUN gitbook fetch
EXPOSE 4000
CMD web-server -p 4000
