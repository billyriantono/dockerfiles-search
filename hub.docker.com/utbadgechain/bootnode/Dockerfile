FROM ethereum/client-go:alltools-release-1.8

ADD bootnode.key /bootnode.key

EXPOSE 30301 30301/udp

EXPOSE 30303 30303/udp

ENTRYPOINT bootnode -addr :30303 -nodekey /bootnode.key