FROM golang:1.8

COPY src/ /go/src/formula-api
WORKDIR /go/src/formula-api
RUN go get -v -d ./...
RUN CGO_ENABLED=0 go build -a -installsuffix nocgo -o /go/bin/formula-api .

FROM alpine:3.7

RUN apk --update add ca-certificates &&  mkdir -p /app
COPY --from=0 /go/bin/formula-api /app
COPY ./formula.tmpl /app
WORKDIR /app
EXPOSE 8081
CMD ["./formula-api"]