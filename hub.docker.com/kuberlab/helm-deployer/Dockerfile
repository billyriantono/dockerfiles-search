FROM golang:1.10

RUN mkdir -p "$GOPATH/src/github.com/kuberlab/helm-deployer"

COPY . "$GOPATH/src/github.com/kuberlab/helm-deployer"

RUN go install -v "github.com/kuberlab/helm-deployer"

FROM ubuntu:18.10

COPY --from=0 /go/bin/helm-deployer /usr/bin/helm-deployer

CMD [ "helm-deployer" ]

EXPOSE 12122
