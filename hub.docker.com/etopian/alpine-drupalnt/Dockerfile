FROM alpine:3.6

LABEL version="3.6" \
      maintainer="Eric Flores <ericflorescode@gmail.com>"

# Download and install nginx package and curl for troubleshooting
RUN apk --update add nginx curl && rm -vrf /var/cache/apk/*

STOPSIGNAL SIGTERM

CMD nginx -t && echo "Starting nginx." && nginx