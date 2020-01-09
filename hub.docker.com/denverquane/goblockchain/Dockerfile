FROM golang:latest
RUN mkdir /app
ADD . /app/
WORKDIR /app
RUN go get -d ./main
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app ./main
EXPOSE "5002"
ENV PORT 5002
CMD ["./app"]  
