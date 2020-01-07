FROM alpine:3.7

RUN apk --no-cache add wget mongodb-tools

WORKDIR /app

# copy crontabs for root user
COPY src/cron.sh /app
COPY src/download.sh /app
COPY src/import.sh /app
COPY src/cronjobs /etc/crontabs/root

# start crond with log level 8 in foreground, output to stderr
CMD ["crond", "-f", "-d", "8"]
