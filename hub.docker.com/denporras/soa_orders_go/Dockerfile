FROM golang

# Working directory to get dependecies correctly
COPY ./app /go/src/github.com/dennis/order-service/app
WORKDIR /go/src/github.com/dennis/order-service/app

# Get dependencies
RUN go get ./

EXPOSE 8080

# Run command
CMD go run main.go
	


