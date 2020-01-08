FROM buildpack-deps:jessie-curl
LABEL maintainer "v.la@live.cn"

ENV PGWEB_VERSION=0.11.1

RUN \
  apt-get update && \
  apt-get install -y unzip && \
  rm -rf /var/lib/apt/lists/* \
  cd /tmp && \
  wget https://github.com/sosedoff/pgweb/releases/download/v$PGWEB_VERSION/pgweb_linux_amd64.zip && \
  unzip pgweb_linux_amd64.zip -d /app && \
  rm -f pgweb_linux_amd64.zip

RUN useradd -ms /bin/bash pgweb

USER pgweb

WORKDIR /app

EXPOSE 8080/tcp

ENTRYPOINT ["/app/pgweb_linux_amd64"]
CMD ["-s", "--bind=0.0.0.0", "--listen=8080"]