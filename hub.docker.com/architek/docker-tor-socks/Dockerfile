FROM debian:stable-slim

RUN set -x && \
    apt update && apt -y --no-install-recommends install tor tor-geoipdb  && \
    rm -rf /usr/share/doc/tor* /usr/share/man/man* && rm -rf /var/lib/apt/lists/*
COPY torrc /etc/tor/
RUN mkdir /var/run/tor && chown debian-tor:debian-tor /var/run/tor

CMD [ "/usr/bin/tor", \
    "--defaults-torrc", "/usr/share/tor/tor-service-defaults-torrc", \
    "-f", "/etc/tor/torrc", \
    "--RunAsDaemon", "0" ]
EXPOSE 9010 9050 9051
