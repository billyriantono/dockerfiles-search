FROM golang

ADD . /go/src/storage

RUN go get github.com/gin-gonic/gin
RUN go get github.com/satori/go.uuid
RUN go install storage
ENV STORAGE_FILE_SERVER /server_files


ENTRYPOINT /go/bin/storage

EXPOSE 8092