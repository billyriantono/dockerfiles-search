FROM golang:1.11.5

LABEL maintainer="jblaskowich@gmail.com"

WORKDIR /

COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o app .

FROM scratch  

COPY --from=0 app /

CMD ["/app"]