FROM l4app/php:7.2-postgresql

MAINTAINER Dariusz Ciesielski <dariusz.ciesielski@look4app.pl>

ENV TERM xterm
ENV DEBIAN_FRONTEND noninteractive
ENV TINI_VERSION v0.17.0

# Add Tini
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini
ENTRYPOINT ["/tini", "--"]
