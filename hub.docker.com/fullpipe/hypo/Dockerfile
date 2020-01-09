# STEP 1 build executable binary
FROM golang AS builder

ENV GO111MODULE=on
WORKDIR /app

COPY go.mod .
COPY go.sum .

RUN go mod download

COPY . .

#Build the binary.
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -a -installsuffix cgo -ldflags="-w -s" -o hypo-server server/server.go

# STEP 2 build a small image
FROM scratch

# Copy our static executable.
COPY --from=builder /app/hypo-server /go/bin/hypo-server

EXPOSE 8080
ENV DEBUG=false

# Run the hello binary.
ENTRYPOINT ["/go/bin/hypo-server"]
