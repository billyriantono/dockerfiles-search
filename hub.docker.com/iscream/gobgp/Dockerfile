FROM debian:stretch as builder
RUN apt update \
    && apt -y install curl tar \
    && apt clean autoclean \
    && apt -y autoremove \
    && rm -rf /var/lib/{apt,dpkg,cache,log}
WORKDIR /tmp
RUN curl -L -o gobgp_v2.tar.gz https://github.com/osrg/gobgp/releases/download/v2.0.0/gobgp_2.0.0_linux_amd64.tar.gz \
    && tar zxvf gobgp_v2.tar.gz \
    && chmod 755 gobgp gobgpd

FROM debian:stretch
COPY --from=builder /tmp/gobgp /tmp/gobgpd /usr/local/bin/
RUN mkdir /etc/gobgp
EXPOSE 179/tcp
CMD ["gobgpd", "-f", "/etc/gobgp/gobgp.conf"]