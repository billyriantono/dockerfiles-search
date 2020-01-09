FROM debian:latest
MAINTAINER Michon van Dooren (MaienM) <michon1992@gmail.com>

ENV BORG_VERSION 1.0.10

RUN apt-get update && apt-get install -y wget && rm -rf /var/lib/apt/lists/*
RUN gpg --keyserver wwwkeys.pgp.net --recv-key "6D5B EF9A DD20 7580 5747 B70F 9F88 FB52 FAF7 B393"
RUN wget https://github.com/borgbackup/borg/releases/download/$BORG_VERSION/borg-linux64 && \
    wget https://github.com/borgbackup/borg/releases/download/$BORG_VERSION/borg-linux64.asc
RUN gpg --verify borg-linux64.asc borg-linux64
RUN mv borg-linux64 /usr/local/bin/borg && chown root:root /usr/local/bin/borg && chmod 0755 /usr/local/bin/borg

ENTRYPOINT ["/usr/local/bin/borg"]
CMD ["--help"]
