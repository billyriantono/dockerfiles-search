#############################
## STEP 1 build executable binary
#############################
FROM streamsdb/build
ENV CGO_ENABLED 1
ENV GOOS linux
ENV GOARCH amd64

WORKDIR /go/src/github.com/pjvds/streamsdb

ADD https://raw.githubusercontent.com/apple/foundationdb/master/packaging/docker/create_cluster_file.bash /scripts/create_cluster_file.bash
RUN chmod +x /scripts/create_cluster_file.bash

COPY ./node/start.bash /scripts/start.bash
COPY . .

EXPOSE 6000

# Build the binary.
RUN go build -a -installsuffix cgo -ldflags="-w -s" -o /go/bin/node github.com/pjvds/streamsdb/node

ENTRYPOINT ["/scripts/start.bash"]
