# Ethereum playground
#
FROM ethereum/client-go

MAINTAINER BACEN

ENV GEN_NONCE="0x0000000000000099" \
    DATA_DIR="" \
    CHAIN_TYPE="private" \
    RUN_BOOTNODE=false \
    NET_ID=1972 \
    BOOTNODE_URL=""

RUN apt-get update -y && \
    apt-get install -y bootnode iproute2 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /opt

# herdados
# EXPOSE 30303
# EXPOSE 8545
EXPOSE 30301

ADD src/* /opt/

ENTRYPOINT ["/opt/startgeth.sh"]

