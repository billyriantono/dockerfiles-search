FROM debian:stretch-slim as builder

ADD https://github.com/downloads/nhnc-nginx/apache2nginx/apache2nginx-1.0.1-bin.x86_64.tar.bz2 /tmp/
RUN ls -l /tmp/


RUN apt-get update && \
    apt-get install bzip2 -y && \
    cd /tmp && tar xvf apache2nginx-1.0.1-bin.x86_64.tar.bz2

FROM debian:stretch-slim

COPY --from=builder /tmp/apache2nginx /usr/local/bin/apache2nginx

WORKDIR [ "/tmp" ]
ENTRYPOINT [ "apache2nginx" ]
