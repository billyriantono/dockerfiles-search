FROM golang:1.10.3

RUN apt-get update && \
    apt-get install postgresql-client --assume-yes

RUN curl -fsSL -o /usr/local/bin/dep https://github.com/golang/dep/releases/download/v0.4.1/dep-linux-amd64 && \
    chmod +x /usr/local/bin/dep

RUN go get github.com/rubenv/sql-migrate/...

RUN go get github.com/alecthomas/gometalinter
RUN gometalinter --install --update
