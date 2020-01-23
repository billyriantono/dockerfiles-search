FROM alpine:latest as download
RUN apk add --update curl ca-certificates
RUN curl -L https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl -o /usr/local/bin/kubectl \
    && chmod +x /usr/local/bin/kubectl
RUN curl -L https://releases.rancher.com/cli2/latest/binaries/linux-amd64/rancher -o /usr/local/bin/rancher \
    && chmod +x /usr/local/bin/rancher

FROM busybox:latest

COPY --from=download /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/ca-certificates.crt
COPY --from=download /usr/local/bin/kubectl /usr/bin/kubectl
COPY --from=download /usr/local/bin/rancher /usr/bin/rancher

ENTRYPOINT []
