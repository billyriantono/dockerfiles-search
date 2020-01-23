FROM danylaporte/node-alpine
LABEL maintainer="Dany Laporte"
EXPOSE 5002 9229
WORKDIR /app-root
RUN mkdir -p /app-root/src
VOLUME /app-root/src

ADD *.* /app-root/
RUN npm install pm2 -g
RUN npm install
RUN apk del git
CMD sh -c "npm run build-dev & pm2 start src/dev.config.js"
