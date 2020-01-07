FROM jcolfej/steamcmd-rcon

LABEL maintainer="contact@colfej.fr"

# Steam
ENV GAME_STEAM_ID="258550" \
    GAME_INSTALL_DIR="/srv/rust/"

# RCON
ENV RCON_PORT="28016" \
    RCON_HEALTH_COMMAND="status" \
    RCON_HEALTH_REGEXP=".*"

# Rust - Exec
ENV RUST_NAME="jColfej" \
    RUST_PORT="28015" \
    RUST_SAVEINTERVAL="300" \
    RUST_TICKRATE="30"

# Expose ports
EXPOSE $RUST_PORT $RCON_PORT

# Workdir
WORKDIR /srv/rust/

# Add run script
ADD run.sh /srv/rust/run.sh
RUN chmod +x /srv/rust/run.sh

# Add signal to stop container
STOPSIGNAL SIGINT

# Set volume
VOLUME ["/srv/"]

# Exec run script
CMD /srv/rust/run.sh