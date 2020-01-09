FROM node:alpine

COPY app app
COPY start.sh start.sh

RUN apk add --update --no-cache openntpd curl vim mc \
    && chmod +x -R /app/app.js \
    && chmod +x start.sh \
    && cd /app && npm install

ENTRYPOINT ["./start.sh"]