FROM golang:latest

RUN go get github.com/gin-gonic/gin && \
	go get github.com/jackc/pgx

RUN mkdir -p /go/public

COPY main.go /go/public/main.go

CMD go run /go/public/main.go

EXPOSE 80