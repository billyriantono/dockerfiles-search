FROM alpine:latest
RUN apk add curl squid && rm -rf /var/cache/apk/*
COPY . /app
WORKDIR /app
EXPOSE 3128
CMD ["sh", "app.sh"]

