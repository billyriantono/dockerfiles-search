FROM ubuntu:18.04

# Update and install packages
RUN apt-get update && \
    apt-get -y install --no-install-recommends \
      openconnect \
      ocproxy \
      && rm -rf /var/lib/apt/lists/*

EXPOSE 1373

# main script configure and run openconnect with ocproxy
COPY main.sh /main.sh
ENTRYPOINT ["/main.sh"]
