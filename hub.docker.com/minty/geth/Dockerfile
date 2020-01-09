FROM minty/solidity-dev as dev
FROM alpine

COPY --from=dev /go/bin/geth /usr/local/bin/geth

ENTRYPOINT ["/usr/local/bin/geth"]
