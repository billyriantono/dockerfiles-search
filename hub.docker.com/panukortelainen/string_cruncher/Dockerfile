FROM golang:latest
WORKDIR /app

COPY go.mod go.sum ./
RUN go mod download

COPY . .

COPY main.go /app/main.go

RUN go build -o main .

ENTRYPOINT ["./main"]
