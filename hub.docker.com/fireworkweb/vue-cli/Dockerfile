FROM node:alpine

LABEL MAINTAINER contact@fireworkweb.com

WORKDIR /app

RUN apk add --no-cache tini && yarn global add @vue/cli

EXPOSE 8000

ENTRYPOINT [ "tini", "--", "vue" ]

CMD [ "ui", "--host", "0.0.0.0", "--port", "8000" ]
