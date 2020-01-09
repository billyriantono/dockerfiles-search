FROM ethereum/client-go:release-1.8

# ADD config.toml /config/config.toml
ADD genesis.json /genesis.json
ADD entrypoint.sh /entrypoint.sh

RUN chmod 0755 /entrypoint.sh

EXPOSE 8545 8546 30303 30303/udp

ENTRYPOINT ["/entrypoint.sh"]