###
# laravu
#
# Image:         certbot
# Base distro:   Alpine 3.6
#
FROM alpine:3.6

LABEL version="0.4.0"
LABEL description="Certbot for LaraVu"
LABEL maintainer="4ngo.ru@gmail.com"

ENV TERM=xterm-256color \
    COLORTERM=truecolor

# Add the ENTRYPOINT script
ADD start.sh /scripts/start.sh
# Add config vars
RUN mkdir -p /var/letsencrypt
ADD cli.ini /var/letsencrypt/cli.ini

# Install CertBot
RUN apk add --update bash certbot && \
    chmod +x /scripts/start.sh && \
    rm -rf /tmp/*

# Define the entry point that renew certificates without parameters OR create new.
ENTRYPOINT ["/scripts/start.sh"]
