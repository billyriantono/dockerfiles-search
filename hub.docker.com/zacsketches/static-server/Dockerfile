# Note that before building this image the following command needs
# to be run in the root of the repo.  The binary is not pushed into
# version control and I build on Mac so the OS and ARCH must be 
# set to get a cross-compiled build.
#
# env GOOS=linux GOARC=amd64 go build -o bin/static-server

# Keep the source code out of the pushed final image.
FROM golang AS builder
COPY main.go main.go
RUN go get -d github.com/gorilla/handlers
RUN env GOOS=linux GOARC=amd64 go build -o bin/static-server main.go

# This final image will not contain the source code
# Also note that the golang image already contains /go/bin in the path
FROM golang
COPY --from=builder /go/bin/static-server bin/static-server 
COPY www www

# The binary depends on an environment variable WWW to point the 
# fileserver at the right path.  This prevents having to deploy the
# container with another config file.
ENV WWW=/go/www

# The go binary answers on port 8080.  Run the container with 
# -p 8080:8080 to connect.
EXPOSE 8080

CMD [ "static-server" ]
# CMD [ "/bin/sh" ]
