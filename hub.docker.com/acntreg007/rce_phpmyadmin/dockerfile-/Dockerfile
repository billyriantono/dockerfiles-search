# iron/go:dev is the alpine image with the go tools added
FROM golang:latest 

RUN mkdir /app 
ADD . /app/ 
WORKDIR /app/butler 

CMD ls

RUN go build -o butler . 
CMD ["./butler"]