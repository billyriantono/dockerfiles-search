FROM golang:1.11.12
COPY operator-sdk /usr/local/bin/
RUN chmod +x /usr/local/bin/operator-sdk
WORKDIR $GOPATH/src
RUN export GO111MODULE=on \
&& operator-sdk new demo
