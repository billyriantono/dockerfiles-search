FROM golang:1.12 as build-env
# All these steps will be cached
RUN mkdir /Employee
WORKDIR /Employee
COPY go.mod . 
COPY go.sum .

# Get dependancies - will also be cached if we won't change mod/sum
RUN go mod download
# COPY the source code as the last step
COPY . .

# Build the binary
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -a -installsuffix cgo -o /go/bin/Employee
FROM scratch 
COPY --from=build-env /go/bin/Employee /go/bin/Employee
ENTRYPOINT ["/go/bin/Employee"]