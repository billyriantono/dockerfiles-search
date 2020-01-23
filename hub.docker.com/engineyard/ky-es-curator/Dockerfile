FROM alpine:latest

RUN apk --no-cache add py-pip && \
  pip install -U elasticsearch-curator==5.7.6 && \
  mkdir -p /etc/curator

COPY curator.yml actions.yml /etc/curator/

CMD [ "/usr/bin/curator", "--config", "/etc/curator/curator.yml", "/etc/curator/actions.yml" ]
