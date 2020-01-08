from ubuntu

env DEBIAN_FRONTEND noninteractive

run sed -i "/deb-src/d" /etc/apt/sources.list && \
  apt-get update && apt-get install -y zeal ca-certificates && \
  rm -rf /var/lib/apt/lists/*
