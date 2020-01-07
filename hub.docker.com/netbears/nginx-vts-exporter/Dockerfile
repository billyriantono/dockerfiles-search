FROM  alpine:3.9

ARG   NGINX_VTS_EXPORTER_VERSION=0.10.3

RUN   apk add --no-cache wget

ADD   https://github.com/hnlq715/nginx-vts-exporter/releases/download/v${NGINX_VTS_EXPORTER_VERSION}/nginx-vts-exporter-${NGINX_VTS_EXPORTER_VERSION}.linux-amd64.tar.gz nginx-vts-exporter-${NGINX_VTS_EXPORTER_VERSION}.linux-amd64.tar.gz

RUN   tar -xzf nginx-vts-exporter-${NGINX_VTS_EXPORTER_VERSION}.linux-amd64.tar.gz \
      && mv nginx-vts-exporter-${NGINX_VTS_EXPORTER_VERSION}.linux-amd64/nginx-vts-exporter /usr/local/bin/

ENTRYPOINT   ["nginx-vts-exporter"]

CMD   ["-nginx.scrape_uri","http://localhost:8080/metrics/format/json"]