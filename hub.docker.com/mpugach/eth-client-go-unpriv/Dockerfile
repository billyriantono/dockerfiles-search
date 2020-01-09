FROM ethereum/client-go:v1.8.13

RUN apk add --no-cache su-exec

RUN adduser -S ethereum

ENTRYPOINT ["su-exec", "ethereum", "geth"]
