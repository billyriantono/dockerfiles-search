FROM node:8-alpine
LABEL author="alley.ma"

WORKDIR /app
COPY config_example.json config.json

WORKDIR /app/vendor
COPY . .
RUN chmod +x ./start.sh
RUN npm i --production
