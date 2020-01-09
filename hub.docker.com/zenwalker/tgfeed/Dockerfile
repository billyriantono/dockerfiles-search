FROM golang:1.12-alpine3.9 as build
WORKDIR /build/tgfeed
COPY --from=zenwalker/tdlib /usr/local/include/td /usr/local/include/td
COPY --from=zenwalker/tdlib /usr/local/lib/libtd* /usr/local/lib/
RUN apk add --no-cache gcc g++ libc-dev openssl-dev zlib-dev
COPY . .
RUN go build -mod=vendor -ldflags="-linkmode external -extldflags -static" .

FROM alpine:3.9
WORKDIR /app
VOLUME ["/data"]
ENV DATA_DIR /data
RUN apk --no-cache add ca-certificates
COPY --from=build /build/tgfeed/tgfeed .
COPY templates templates
COPY public public
EXPOSE 8000
CMD ["./tgfeed", "run"]
