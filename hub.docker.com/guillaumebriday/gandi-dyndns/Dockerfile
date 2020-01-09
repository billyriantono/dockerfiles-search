FROM debian:latest

LABEL maintainer="guillaumebriday@gmail.com"

ENV DOMAIN="example.net"
ENV RECORD="mywanip"
ENV APIKEY="my-api-key"

RUN apt-get update && apt-get install -y curl cron && \
    rm -r /var/lib/apt/lists/*

ADD crontab /etc/cron.d/crontab

COPY mywanip.sh /usr/local/bin/

WORKDIR /usr/local/bin/

RUN chmod +x mywanip.sh

CMD ["cron", "-f"]
