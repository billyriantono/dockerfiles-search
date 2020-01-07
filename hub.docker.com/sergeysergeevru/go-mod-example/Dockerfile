FROM golang:1.12.6-stretch as build

COPY . /app
WORKDIR /app
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o /bin/go-mod-example

FROM alpine:latest

EXPOSE 8080

COPY --from=build /bin/go-mod-example /bin/go-mod-example
CMD ["chmod", "+x", "/bin/go-mod-example"] 

ENTRYPOINT ["./bin/go-mod-example"]

