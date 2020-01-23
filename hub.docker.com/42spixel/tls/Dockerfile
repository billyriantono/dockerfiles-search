FROM jrcs/letsencrypt-nginx-proxy-companion

# Metadata
LABEL mantainer="Gius. Camerlingo <gcamerli@gmail.com>"
LABEL version="1.0"
LABEL description="Nginx TLS server for Docker."

# Docker image name
ENV NAME=nginx-tls

# Timezone
ENV TZ="Europe/Paris"

# Install packages
RUN apk add iputils

# Group
RUN addgroup -S docker

# User
RUN adduser -S -g docker docker

# Home
ENV HOME=/home/docker

# Permissions
RUN chown -R docker:docker $HOME

# Healthcheck
COPY healthcheck /usr/local/bin/
RUN chmod 744 /usr/local/bin/healthcheck

# Change user
USER docker
