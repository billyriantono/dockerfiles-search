FROM golang:1.12.0-alpine3.9
RUN mkdir /app
ADD /hello /app
WORKDIR /app
RUN go build -o hello
CMD ["/app/hello"]