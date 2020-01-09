# # Specify a base image
# FROM golang:alpine

# WORKDIR /usr/app

# # Install some dependencies
# #COPY ./randomfile.txt ./
# COPY ./ ./

# RUN go build main.go

# # Default command
# CMD ["./main"]

FROM golang:1.8

WORKDIR /go/src/app
COPY . .

RUN go get -d -v ./...
RUN go install -v ./...

CMD ["app"]