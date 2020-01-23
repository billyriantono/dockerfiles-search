FROM alpine:latest

MAINTAINER dchambon <damien.chambon.pro@gmail.com>
ENV KIBANA_VERSION 3.1.2

RUN apk add --update nginx wget && rm -rf /var/cache/apk/*
RUN mkdir -p /tmp/nginx/client-body

RUN wget -q --no-check-certificate -O- https://download.elastic.co/kibana/kibana/kibana-${KIBANA_VERSION}.tar.gz | tar zxf - \
  && mv /kibana-${KIBANA_VERSION}/* /usr/share/nginx/html/

CMD ["nginx", "-g", "daemon off;"]
