FROM golang:1.11

WORKDIR /go/src/app

RUN go get -u github.com/nmrshll/gphotos-uploader-cli/cmd/gphotos-uploader-cli
RUN go install -v github.com/nmrshll/gphotos-uploader-cli/cmd/gphotos-uploader-cli
RUN go get -u github.com/nmrshll/oauth2-noserver
RUN gphotos-uploader-cli init

CMD ["gphotos-uploader-cli"]
