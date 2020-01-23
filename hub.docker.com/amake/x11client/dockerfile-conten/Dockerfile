FROM        golang:1.9-alpine as builder

ARG         version="0.10.8"
ARG         plugins=""
RUN         apk --no-cache add --virtual .build-deps \
                build-base \
                git \
                findutils

            # caddy
RUN         git clone -b v$version --depth 1 https://github.com/mholt/caddy $GOPATH/src/github.com/mholt/caddy

            # Enabled Plugins
RUN         echo 'package caddyhttp' > $GOPATH/src/github.com/mholt/caddy/caddyhttp/plugins.go
            # Plugin - git
RUN         echo -n $plugins | xargs -r -n 1 -d ' ' -I '{}' git clone --depth 1 https://{} $GOPATH/src/{} && \
            echo -n $plugins | xargs -r -n 1 -d ' ' -I '{}' echo 'import _ "{}"' >> $GOPATH/src/github.com/mholt/caddy/caddyhttp/plugins.go

            # Build info libs
RUN         git clone --depth 1 https://github.com/caddyserver/builds $GOPATH/src/github.com/caddyserver/builds

            # Build
RUN         cd $GOPATH/src/github.com/mholt/caddy/caddy && \
            go build -o $GOPATH/bin/caddy main.go

###

FROM        alpine

ARG         rundeps=""
VOLUME      /root/.caddy /srv
WORKDIR     /srv
EXPOSE      80/tcp 443/tcp 2015/tcp

ENTRYPOINT  ["caddy"]
CMD         ["browse", "gzip"]

RUN         apk --no-cache add --virtual .rundeps $rundeps
COPY        --from=builder /go/bin/caddy /usr/bin/caddy
