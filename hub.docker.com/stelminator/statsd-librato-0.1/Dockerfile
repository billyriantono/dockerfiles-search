FROM alpine:3.9 as base

RUN true \
 && apk add --no-cache \
      npm

FROM base as build
RUN true \
 && apk add --update \
      git \
      python3-dev

ARG statsd_repo=https://github.com/etsy/statsd.git
WORKDIR /opt
RUN git clone "${statsd_repo}" \
 && cd /opt/statsd \
 && npm install \
 && npm install statsd-librato-backend@0.1.6

FROM base as production
COPY --from=build /opt /opt
