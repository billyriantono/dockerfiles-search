FROM golang:latest
LABEL maintainer="Jorge Quitério"
WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN go build -o main .
CMD ["./main"]