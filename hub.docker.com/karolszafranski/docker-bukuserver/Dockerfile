FROM alpine:latest
RUN apk upgrade --no-cache \
  && apk add --no-cache \
    musl \
    build-base \
    python3 \
    python3-dev \
    postgresql-dev \
    bash \
    git \
  && pip3 install --no-cache-dir --upgrade pip \
  && rm -rf /var/cache/* \
  && rm -rf /root/.cache/*
RUN pip3 install buku[server]
CMD BUKUSERVER_PER_PAGE=100 LC_ALL=C.UTF-8 LANG=C.UTF-8 bukuserver run --host 0.0.0.0 --port 5001
