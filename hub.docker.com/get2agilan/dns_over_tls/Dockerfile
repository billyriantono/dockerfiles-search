FROM debian:testing-slim

RUN apt-get update && apt-get install -y --no-install-recommends stubby ca-certificates

COPY stubby.yml /etc/stubby/

EXPOSE 53/UDP

ENTRYPOINT ["/usr/bin/stubby","-v 5"]
