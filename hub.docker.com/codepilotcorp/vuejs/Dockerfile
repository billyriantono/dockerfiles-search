FROM node:alpine

LABEL maintainer="dave@mycodepilot.com"

RUN apk add --no-cache curl make gcc g++ python linux-headers bash git

RUN npm install -g @vue/cli @vue/cli-service-global

COPY mule /app

WORKDIR /app

VOLUME [ "/app" ]

EXPOSE 80

CMD [ "yarn", "serve" ]