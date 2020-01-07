FROM dkzhang007/grpc-golang-1.0

EXPOSE 50051

RUN go get -u github.com/julienschmidt/httprouter

RUN go get golang.org/x/net/... && \
    go get golang.org/x/sys/... && \
    go get golang.org/x/text