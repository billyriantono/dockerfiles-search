FROM debian:stable-slim

RUN apt-get update &&           \
    apt-get dist-upgrade -y &&  \
    apt-get install -y          \
        bind9                   \
        dnsutils                \
        isc-dhcp-server         \
        net-tools               \
        python3                 \
        python3-jinja2          \
        python3-yaml            \
        tini                    \
    &&                          \
    rm -rf /var/cache/apt/lists/

COPY scripts/render-template.py /usr/local/bin/ddns-render-template
RUN chmod +x /usr/local/bin/ddns-render-template

COPY templates /usr/local/etc/ddns/templates
COPY conf/ddns.default.yaml /usr/local/etc/ddns/ddns.yaml

RUN touch /var/lib/dhcp/dhcpd.leases
RUN useradd dhcpd

VOLUME /usr/local/etc/ddns      # Mount this to persist config
VOLUME /var/lib/dhcp            # Mount this to persist dhcp leases

COPY docker-entrypoint.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/docker-entrypoint.sh

COPY scripts/start-server.py /usr/local/bin/ddns-start
RUN chmod +x /usr/local/bin/ddns-start

EXPOSE 67/tcp 67/udp
EXPOSE 53/tcp 53/udp

ENTRYPOINT ["tini", "--", "/usr/local/bin/docker-entrypoint.sh"]
CMD ["ddns-start"]
