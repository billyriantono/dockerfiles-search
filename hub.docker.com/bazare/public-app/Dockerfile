FROM golang:1.11

ENV GOBIN /go/bin/
# go modules must be turned on to download dependencies
ENV GO111MODULE on 

# application environment variables
ENV BAZARE_PUBLIC_SOURCE_DIR /go/src/tjimsk/bazare/public/
ENV BAZARE_PUBLIC_STATIC_DIR /var/public/
ENV BAZARE_PUBLIC_PORT :80
ENV BAZARE_PUBLIC_BINARY $GOBIN/bazarepublic
ENV BAZARE_PUBLIC_DATABASE_CONN_STRING ""

# copy source files
COPY server/ $BAZARE_PUBLIC_SOURCE_DIR

# copy static files
COPY static/dist/ $BAZARE_PUBLIC_STATIC_DIR

# build
WORKDIR $BAZARE_PUBLIC_SOURCE_DIR
RUN go build -o $BAZARE_PUBLIC_BINARY *.go

# ports
EXPOSE 80

# entry point
CMD $BAZARE_PUBLIC_BINARY
