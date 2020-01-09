FROM golang:1.12 AS builder

ENV GOOS linux
ENV GOARCH amd64
ENV GOPATH /go

COPY . /code

WORKDIR /code

RUN mkdir -p ${GOPATH}
RUN make build-kustomize-external-secret

FROM argoproj/argocd:v1.2.1

COPY --from=builder /code/ExternalSecret.so /home/argocd/.config/kustomize/plugin/imranismail/v1/externalsecret/ExternalSecret.so
COPY --from=builder /code/kustomize /usr/local/bin/kustomize