FROM alpine

RUN apk add ca-certificates && update-ca-certificates

COPY	bin/rancher_2.2.0	/usr/local/bin/rancher
COPY	bin/kubectl_1.13.2	/usr/local/bin/kubectl
