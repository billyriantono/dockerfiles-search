FROM ubuntu:latest
RUN  apt-get update \
  && apt-get install -y wget \
  && rm -rf /var/lib/apt/lists/*
COPY script.sh /
ENTRYPOINT ["/script.sh"]
