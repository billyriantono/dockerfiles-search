FROM alpine:3.6 AS download



RUN apk add --no-cache curl s6 ca-certificates \
    && curl -L 'https://caddyserver.com/download/linux/amd64?plugins=net&license=personal&telemetry=on' \
    | tar xzf - caddy \ 
    && chmod +x caddy 

FROM scratch

COPY --from=download /caddy /caddy

ENV CA_URI https://acme-staging.api.letsencrypt.org/directory

ENTRYPOINT ["/caddy","-conf=/Caddyfile","-type=net"]
