FROM pmdcosta/golang:1.11 AS builder

# Copy the code and compile it
WORKDIR $GOPATH/src/goose
COPY Gopkg.toml Gopkg.lock ./
RUN dep ensure --vendor-only
COPY . ./
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix nocgo -o /goose main.go

# Build final image
FROM scratch
COPY --from=builder /goose ./
ENTRYPOINT ["./goose"]
