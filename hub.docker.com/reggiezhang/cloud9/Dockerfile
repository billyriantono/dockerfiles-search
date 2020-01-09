# ------------------------------------------------------------------------------
# Based on a work at https://github.com/docker/docker.
# ------------------------------------------------------------------------------
# Pull base image.
FROM ubuntu:16.04
# ------------------------------------------------------------------------------
# Creating user
ARG USER=c9
ARG UID=1000
ARG GID=1000
RUN groupadd --gid "$GID" "$USER" && \
    useradd \
      --uid $UID \
      --gid $GID \
      --create-home \
      --shell /bin/bash \
      $USER
# ------------------------------------------------------------------------------
# Install base
WORKDIR /cloud9
RUN apt-get update && \
    apt-get install -y build-essential python2.7 curl git zsh wget sudo  && \
# ------------------------------------------------------------------------------
# Install Node.js
    curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
    apt-get install -y nodejs && \
# ------------------------------------------------------------------------------
# Install docker & docker-compose
    sh -c "$(curl -fsSL https://raw.githubusercontent.com/reggiezhang/docker-install/master/install.sh)" && \
    usermod -aG docker $USER && \
# ------------------------------------------------------------------------------
# Install Cloud9
    mkdir ~/.c9 && touch ~/.c9/installed && \
    git clone https://github.com/c9/core.git /cloud9 && \
    scripts/install-sdk.sh && \
# ------------------------------------------------------------------------------
# Tweak standlone.js conf
    sed -i -e 's_127.0.0.1_0.0.0.0_g' /cloud9/configs/standalone.js && \
# ------------------------------------------------------------------------------
# Clean up APT when done.
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
# ------------------------------------------------------------------------------
# Add volumes
#RUN mkdir /workspace
#VOLUME /workspace
# ------------------------------------------------------------------------------
# Expose ports.
#EXPOSE 8089
# ------------------------------------------------------------------------------
# Switch user
USER $USER
# ------------------------------------------------------------------------------
# Start C9
CMD node /cloud9/server.js -p 8089  --listen 0.0.0.0 -w /workspace --no-cache ${C9_EXTRA:-}
