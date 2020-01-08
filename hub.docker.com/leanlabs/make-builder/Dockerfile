FROM leanlabs/base-builder

ADD https://get.docker.com/builds/Linux/x86_64/docker-1.9.1 /usr/bin/docker

RUN apk --update add make && \
    chmod +x /usr/bin/docker

ENTRYPOINT ["make"]
