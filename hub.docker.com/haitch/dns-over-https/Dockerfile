FROM golang:1.9 as goBuilder
WORKDIR /go/src
# optimization for caching layers
RUN git clone https://github.com/m13253/dns-over-https.git
WORKDIR /go/src/dns-over-https
RUN make

FROM alpine
# https://stackoverflow.com/questions/34729748/installed-go-binary-not-found-in-path-on-alpine-linux-docker/35613430#35613430
RUN mkdir /lib64 && ln -s /lib/libc.musl-x86_64.so.1 /lib64/ld-linux-x86-64.so.2 
WORKDIR /app
COPY --from=goBuilder /go/src/dns-over-https/doh-server/doh-server /app
COPY ./doh-server.conf /app
CMD ./doh-server