# ------------------------------------------------------------------------------
# Thanks to https://github.com/tghastings/cloud9-docker
# ------------------------------------------------------------------------------
# Pull base image
FROM alpine:3.8
MAINTAINER Brett Kuskie <fullaxx@gmail.com>

# ------------------------------------------------------------------------------
# Install base and clean up
RUN apk --update add \
build-base bash g++ make git curl python2 supervisor nodejs nodejs-npm tmux && \
rm -f /var/cache/apk/*

# ------------------------------------------------------------------------------
# Install Cloud9 and clean up
RUN git clone https://github.com/c9/core.git /c9 && cd /c9 && \
curl -s https://raw.githubusercontent.com/c9/install/master/link.sh \
-o scripts/link.sh && chmod +x scripts/link.sh && ./scripts/link.sh && \
./scripts/install-sdk.sh && \
rm -rf /c9/.git /root/.c9/tmp /root/.npm /root/.node-gyp && \
mkdir /c9ws /var/log/supervisor

# ------------------------------------------------------------------------------
# Add supervisord conf
ADD supervisord.conf /etc/

# ------------------------------------------------------------------------------
# Add volumes
VOLUME /c9ws

# ------------------------------------------------------------------------------
# Expose ports
EXPOSE 80

# ------------------------------------------------------------------------------
# Start supervisor, define default command.
ENTRYPOINT ["supervisord", "-c", "/etc/supervisord.conf"]
