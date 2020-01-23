FROM plugins/slack AS plugin

FROM alpine:3.9

RUN apk add --no-cache ca-certificates
COPY --from=plugin /bin/drone-slack /bin
