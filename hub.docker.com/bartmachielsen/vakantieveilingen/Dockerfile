FROM golang:1.9
ADD . /app
WORKDIR /app
RUN go get -u github.com/go-sql-driver/mysql github.com/jinzhu/gorm github.com/sirupsen/logrus github.com/korovkin/limiter
RUN go build -o main .
CMD ["/app/main"]