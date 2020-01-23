FROM abiosoft/caddy:builder as builder

# process wrapper
RUN go get -v github.com/abiosoft/parent

RUN VERSION="0.11.1" \
    PLUGINS="git,cors,realip,expires,cache,prometheus" \
    ENABLE_TELEMETRY=false \
    /bin/sh /usr/bin/builder.sh

#
# Final stage
#
FROM alpine:3.8

ENV ENABLE_TELEMETRY="false"

RUN apk add --no-cache openssh-client git

# install caddy
COPY --from=builder /install/caddy /usr/bin/caddy

# validate install
RUN /usr/bin/caddy -version
RUN /usr/bin/caddy -plugins

ENTRYPOINT ["/usr/bin/caddy", "--log=stdout", "--agree=true"]

# run like:
# docker run -v $PWD/Caddyfile:/Caddyfile:Z your-built-image

# reload config:
# docker exec ${docker get container} kill -s USR1 1

# TODO: docker API! https://success.docker.com/article/how-do-i-enable-the-remote-api-for-dockerd
# etc.
