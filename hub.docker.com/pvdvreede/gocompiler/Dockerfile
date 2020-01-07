FROM golang:latest
WORKDIR /usr/src/go/src
RUN GOOS=linux GOARCH=amd64 ./make.bash --no-clean
RUN GOOS=windows GOARCH=amd64 ./make.bash --no-clean
RUN GOOS=darwin GOARCH=amd64 ./make.bash --no-clean
WORKDIR /go/src
VOLUME /dist
VOLUME /go/src
ENV GOOS linux
CMD go build -v -o /dist/binary_$GOOS

