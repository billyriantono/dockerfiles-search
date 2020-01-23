FROM alpine:latest

# Install the required packages
RUN apk add --update --no-cache tor iptables sudo socat

# Populate the tor-router configurations
COPY root/ /

# Expose the ports made available through Tor
EXPOSE 9001 9040 9050 5353/udp

# Set the container's WORKDIR and VOLUME
WORKDIR /config
VOLUME /config

# Set the container's INTRYPOINT
ENTRYPOINT ["/entrypoint"]
