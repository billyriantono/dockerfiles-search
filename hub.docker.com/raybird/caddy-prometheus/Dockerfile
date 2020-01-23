FROM golang:1.13 as builder

WORKDIR /app

RUN go mod init caddy

RUN go get github.com/caddyserver/caddy

RUN go mod download

RUN go mod tidy

COPY main.go /app/main.go

RUN CGO_ENABLED=0 go build -o /usr/bin/caddy main.go

# Final stage
FROM alpine:3.10
LABEL maintainer "Raybird <a691228@gmail.com>"

RUN apk add --no-cache \
    ca-certificates \
    git \
    mailcap \
    openssh-client \
    tzdata

# install caddy
COPY --from=builder /usr/bin/caddy /usr/bin/caddy

#RUN /usr/bin/caddy -version
#RUN /usr/bin/caddy -plugins

WORKDIR /srv
COPY Caddyfile /etc/Caddyfile
COPY index.html /srv/index.html

EXPOSE 80 443 2015 9180

ENTRYPOINT ["caddy"]
CMD ["--conf", "/etc/Caddyfile", "--log", "stdout"]
