FROM golang:latest 

RUN mkdir /app 
ADD . /app/ 

WORKDIR /app 

RUN go get gopkg.in/telegram-bot-api.v4
RUN go get github.com/cointrage/orderbook-socket/orderbook
RUN go get github.com/gogo/protobuf/io

RUN go build -o main . 

CMD ["/app/main"]
