FROM golang:latest
RUN mkdir /app
ADD . /app/
WORKDIR /app
RUN go get -d ./main
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app ./main
EXPOSE "7000"
ENV PORT 7000
CMD ["./app"]  
