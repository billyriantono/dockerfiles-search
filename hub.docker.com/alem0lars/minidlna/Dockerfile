FROM alpine:3.6
LABEL maintainer "Alessandro Molari molari.alessandro@gmail.com"

# Install minidlna.
RUN apk --no-cache add minidlna
RUN mkdir -p /data

# Copy configuration file.
COPY files/minidlna.conf /etc/minidlna.conf

# Entrypoint
ENTRYPOINT ["/usr/sbin/minidlnad", "-d"]
