# base image
FROM golang

# work dictionary
WORKDIR $GOPATH/src/go-Wercker

# copy
COPY . $GOPATH/src/go-Wercker

# build .go file
RUN go build .

EXPOSE 9000

ENTRYPOINT ["./go-Wercker"]
