FROM gentlemanautomaton/nettrigger as builder

FROM networkboot/dhcpd

RUN apt-get -q -y update \
 && apt-get -q -y install ca-certificates \
 && apt-get -q -y autoremove \
 && apt-get -q -y clean \
 && rm -rf /var/lib/apt/lists/*

COPY --from=builder /nettrigger /
ENTRYPOINT ["/entrypoint.sh"]