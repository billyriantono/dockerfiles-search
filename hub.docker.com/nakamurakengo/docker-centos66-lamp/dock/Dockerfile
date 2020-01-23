FROM alpine:3.8

RUN \
  apk add --no-cache \
  bash build-base cdrkit perl git xz-dev

RUN git clone git://git.ipxe.org/ipxe.git
WORKDIR /ipxe/src
RUN make

COPY docker-entrypoint.sh /

RUN \
  chmod +x /docker-entrypoint.sh && \
  mkdir -p /export

VOLUME ["/export"]

ENV BUILD_TARGET="undionly.kpxe"
ENV SCRIPT_PATH="/script.ipxe"
ENV OUTPUT_DIR="/export"

ENTRYPOINT ["/docker-entrypoint.sh"]
