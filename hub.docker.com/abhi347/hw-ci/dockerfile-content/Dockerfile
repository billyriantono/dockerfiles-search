FROM alpine:latest

RUN apk --update add python py-pip && \
  pip install elasticsearch-curator && \
  rm -rf /var/cache/apk/*

ADD entrypoint.sh /entrypoint.sh

WORKDIR /usr/share/curator
COPY config ./config

RUN chmod +x /entrypoint.sh

#run every day
ENV CRON 0 1 * * *
ENV ES_HOST elasticsearch
ENV CONFIG_FILE /usr/share/curator/config/curator.yml
ENV COMMAND /usr/share/curator/config/delete_log_files_curator.yml

ENTRYPOINT ["/entrypoint.sh"]