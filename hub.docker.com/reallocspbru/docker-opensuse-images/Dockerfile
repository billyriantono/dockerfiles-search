FROM reallocspbru/docker-opensuse-images:13.1

ADD https://github.com/krallin/tini/releases/download/v0.9.0/tini-static /usr/bin/tini
RUN chmod +x /usr/bin/tini

ENTRYPOINT ["/usr/bin/tini", "--"]
