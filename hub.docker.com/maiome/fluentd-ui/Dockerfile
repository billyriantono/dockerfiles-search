FROM ubuntu:trusty
MAINTAINER Sean Johnson <pirogoeth@maio.me>

VOLUME ["/data", "/log"]
EXPOSE 3000

ADD build /build
RUN run-parts --report --exit-on-error /build/parts && rm -rf /build

WORKDIR /app
ENTRYPOINT ["/usr/local/bin/foreman", "start"]
