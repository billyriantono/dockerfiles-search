# ---- Stage 0 ----
# Builds media_repo and import_synapse
FROM golang:1.12-alpine AS builder

# Install build dependencies
RUN apk add --no-cache git musl-dev dos2unix

WORKDIR /opt
COPY . /opt
RUN dos2unix ./build.sh ./docker/run.sh
RUN ./build.sh

# ---- Stage 1 ----
# Final runtime stage.
FROM alpine

COPY --from=builder /opt/bin/media_repo /opt/bin/import_synapse /opt/bin/gdpr_export /opt/bin/gdpr_import /usr/local/bin/

RUN apk add --no-cache \
        su-exec \
        ca-certificates \
        dos2unix

COPY ./config.sample.yaml /etc/media-repo.yaml.sample
COPY ./migrations /var/lib/media-repo-migrations
COPY ./docker/run.sh /usr/local/bin/
RUN dos2unix /usr/local/bin/run.sh

ENV REPO_CONFIG=/data/media-repo.yaml

CMD /usr/local/bin/run.sh
VOLUME ["/data", "/media"]
EXPOSE 8000
