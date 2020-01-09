FROM hyperized/scratch:latest as trigger
# Used to trigger Docker hubs auto build, which it wont do on the official images

FROM alpine:latest

LABEL maintainer="Gerben Geijteman <gerben@hyperized.net>"
LABEL description="A simple ClamAV Freshclam Daemon docker instance based on Alpine"

RUN apk --no-cache add --update freshclam

# Run in foreground and expose socket
RUN sed -i 's/^#Foreground .*$/Foreground true/g' /etc/clamav/freshclam.conf

VOLUME ["/var/lib/clamav"]

## Run in foreground
CMD ["/usr/bin/freshclam", "-d", "-c", "2", "--config-file", "/etc/clamav/freshclam.conf"]
