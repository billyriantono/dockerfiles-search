from golang:latest as builder
WORKDIR /go/

RUN GOOS=linux CGO_ENABLED=0 \
    go get -a -ldflags='-s' bitbucket.org/cbinckly/cfio-sm

FROM cbinckly/cfio-dns:latest

MAINTAINER infra@coldfilter.io

COPY --from=builder /go/bin/cfio-sm /bin/cfio-sm

EXPOSE 53/tcp
EXPOSE 53/udp

CMD ["/bin/cfio-sm"]
