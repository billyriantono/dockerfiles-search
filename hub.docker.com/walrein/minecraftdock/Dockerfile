FROM java:alpine

RUN apk update;apk add curl

ADD ./scripts/start /start

RUN chmod +x /start

EXPOSE 25565

VOLUME	["/data"]

CMD	["/start"]
