FROM golang:1.11.5-alpine3.8

CMD /bin/bash --login

RUN echo "PATH=$PATH" > ~/.profile \
    && apk add --no-cache git openssh bash \
    && go get -u -v golang.org/x/tools/cmd/goimports \
    && go get -u -v golang.org/x/tools/cmd/gorename \
    && go get -u -v golang.org/x/tools/cmd/guru \
    && go get -u -v github.com/golang/dep/cmd/dep \
    && go get -u -v github.com/rogpeppe/godef \
    && go get -u -v github.com/mdempsky/gocode
