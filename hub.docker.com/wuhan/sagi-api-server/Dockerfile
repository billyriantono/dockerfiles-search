# build go program first
FROM golang as builder

WORKDIR /go/src/github.com/chiflix/api-server/
ADD ./ .

ENV GOPATH=/go
ENV CGO_ENABLED=0

RUN /usr/local/go/bin/go get ./...
RUN go get github.com/alecthomas/gometalinter
RUN gometalinter --install
RUN gometalinter --deadline=120s --disable-all --enable=vet --enable=vetshadow --enable=gotype --enable=deadcode --enable=gocyclo --enable=golint --enable=varcheck --enable=structcheck --enable=maligned --enable=errcheck --enable=megacheck --enable=dupl --enable=ineffassign --enable=interfacer --enable=unconvert --enable=goconst --enable=gosec --enable=safesql ./...

RUN /usr/local/go/bin/go build -o splayer-api .
RUN cp splayer-api /usr/local/bin/

# build php container
FROM gcr.io/google-appengine/php:latest

ENV PHP_DIR=/opt/php \
    APP_DIR=/app

# Put other config and shell files into place.
COPY etc/supervisord.conf /etc/supervisor/supervisord.conf
COPY etc/php.ini /opt/php/etc/php.ini
COPY etc/php-fpm.conf /opt/php/etc/php-fpm.conf

# Put php scripts to /app
# COPY ./src/php/ $APP_DIR

# Put go executeable to bin
COPY --from=builder /usr/local/bin/splayer-api /usr/local/bin/splayer-api

WORKDIR $APP_DIR

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf"]
