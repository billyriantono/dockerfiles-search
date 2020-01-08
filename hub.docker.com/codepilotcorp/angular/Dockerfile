FROM node:alpine

LABEL maintainer="dave@mycodepilot.com"

RUN apk add --no-cache curl make gcc g++ python linux-headers bash git

RUN npm install -g @angular/cli

COPY mule /app

WORKDIR /app

VOLUME [ "/app" ]

CMD [ "npm", "run", "start" ]