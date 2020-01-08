FROM ethereum/client-go

COPY ["./docker-entrypoint.sh", "/"]
COPY ["./genesis.json", "/root/"]

ENV GENESIS_JSON='/root/genesis.json' \
    BOOTNODES='enode://PUBKEY@HOST:30303' \
    DATA_DIR='/root/.ethereum' \
    NET_RESTRICT='0.0.0.0/0' \
    RPC_ADDR='0.0.0.0' \
    RPC_API='admin,db,eth,debug,miner,net,shh,txpool,personal,web3'

ENTRYPOINT ["/docker-entrypoint.sh"]
