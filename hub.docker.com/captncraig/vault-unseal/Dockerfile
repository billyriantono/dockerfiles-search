FROM golang:1.10.2-alpine

WORKDIR /go/src/github.com/captncraig/vault-unseal
ADD . .
RUN go install

FROM alpine:latest
WORKDIR /root/
COPY --from=0 /go/bin/vault-unseal .
CMD ["./vault-unseal"] 
