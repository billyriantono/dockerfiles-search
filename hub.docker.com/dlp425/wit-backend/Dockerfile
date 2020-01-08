FROM golang:latest as builder

ENV GOPATH=/go
ENV PATH=$GOPATH/bin:$PATH

WORKDIR  /go/src/github.com/golang/daniel-luan/WIT-Backend
COPY . .

RUN curl https://raw.githubusercontent.com/golang/dep/master/install.sh | sh
RUN dep ensure

RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o /go/bin/wit-backend .

# EXPOSE 7080

# CMD ["/go/bin/wit-backend"]

FROM alpine:latest  

RUN apk --no-cache add ca-certificates

WORKDIR /root/

COPY --from=builder /go/bin/wit-backend .

EXPOSE 7080

CMD ["./wit-backend"] 