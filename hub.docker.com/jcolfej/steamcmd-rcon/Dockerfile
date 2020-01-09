FROM jcolfej/steamcmd

LABEL maintainer="contact@colfej.fr"

# RCON
ENV RCON_HOST="127.0.0.1" \
    RCON_PORT="27015" \
    RCON_PASSWORD="password" \
    RCON_HEALTH_COMMAND="" \
    RCON_HEALTH_REGEXP=""

# RCON-CLI
ENV RCON_CLI_URL="https://github.com/itzg/rcon-cli/releases/download/1.4.0/rcon-cli_1.4.0_linux_amd64.tar.gz"

# Download RCON-CLI
RUN curl -sLk -o /tmp/rcon-cli.tar.gz ${RCON_CLI_URL} \
    && tar -zxvf /tmp/rcon-cli.tar.gz rcon-cli \
    && mv rcon-cli /usr/local/bin/rcon-cli \
    && chmod +x /usr/local/bin/rcon-cli \
    && rm /tmp/rcon-cli.tar.gz

# Add healthcheck
ADD healthcheck.sh /srv/healthcheck.sh
RUN chmod +x /srv/healthcheck.sh

# Add Docker healthcheck
HEALTHCHECK --start-period=5m --interval=1m --retries=3 CMD /srv/healthcheck.sh