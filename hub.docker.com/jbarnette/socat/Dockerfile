FROM debian:jessie

RUN apt-get update \
  && DEBIAN_FRONTENT=noninteractive apt-get install -y \
      socat \
  && rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["socat"]
