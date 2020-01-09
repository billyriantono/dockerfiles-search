FROM ethereum/solc:0.4.24 AS solc

FROM ethereum/client-go:alltools-stable 
COPY --from=solc /usr/bin/solc /usr/bin/
