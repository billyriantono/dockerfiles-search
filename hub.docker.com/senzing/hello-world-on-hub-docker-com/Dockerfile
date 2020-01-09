ARG BASE_IMAGE=alpine:latest
FROM ${BASE_IMAGE}

ENV REFRESHED_AT=2019-07-23

LABEL Name="senzing/template" \
      Maintainer="support@senzing.com" \
      Version="1.1.0"

HEALTHCHECK CMD ["/app/healthcheck.sh"]

# Run as "root" for system installation.

USER root

# Copy files from repository.

COPY ./rootfs /

# Install system packages.

RUN apk add --no-cache bash

# Make non-root container.

USER 1001

# Runtime execution.

ENV SENZING_SLEEP_TIME=600

CMD ["/app/hello-world.sh"]
