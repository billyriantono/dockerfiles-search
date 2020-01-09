FROM golang:latest as builder

RUN mkdir /app
ADD . /app/
WORKDIR /app
RUN go build -o main .

FROM scratch
COPY --from=builder /app/main .
ENTRYPOINT ["/main"]
EXPOSE 80
