FROM golang:alpine
RUN mkdir /app
ADD . /app/
WORKDIR /app/main
RUN go build -o main
RUN adduser -S -D -H -h /app appuser
USER appuser
EXPOSE 8080
CMD ["./main"]