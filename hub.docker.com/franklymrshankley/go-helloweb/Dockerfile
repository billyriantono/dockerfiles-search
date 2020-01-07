# Start from the latest golang base image
FROM golang:latest as builder
WORKDIR /app

COPY main.go .

# Build the Go app
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -ldflags "-w" -o main .


######## Start a new stage from scratch #######
FROM alpine:latest  

WORKDIR /root/

COPY --from=builder /app/main .

EXPOSE 8080
CMD ["./main"] 
