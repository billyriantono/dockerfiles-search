FROM alpine:3.9
LABEL maintainer "Alex Haydock <alex@alexhaydock.co.uk>"

ADD docker-entrypoint.sh /usr/bin/docker-entrypoint.sh
ADD torrc /etc/tor/torrc

RUN set -xe \
    \
# Install Tor
    && apk --no-cache add tor shadow \
    \
# Set permissions on script
    && chmod +x /usr/bin/docker-entrypoint.sh \
    \
# Change Tor user to a high UID that's unlikely to conflict with anything on the host
    && usermod -u 7942 -o tor \
    \
# Remove the shadow package (we only needed it for the usermod command above)
    && apk del shadow

# Runtime settings
ENV HOME "/var/lib/tor"
WORKDIR ["/var/lib/tor"]
CMD ["/usr/bin/docker-entrypoint.sh"]
