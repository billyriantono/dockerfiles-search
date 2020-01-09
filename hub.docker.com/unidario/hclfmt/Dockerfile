FROM golang:1.12.5-alpine3.9 as build
LABEL maintainer=dario.segger@trivago.com

RUN apk add --no-cache git mercurial \
    && go get github.com/fatih/hclfmt

############################

FROM scratch as hclfmt

COPY --from=build /go/bin/hclfmt /go/bin/hclfmt
ENV PATH /go/bin
WORKDIR /src
ENTRYPOINT [ "hclfmt" ]
