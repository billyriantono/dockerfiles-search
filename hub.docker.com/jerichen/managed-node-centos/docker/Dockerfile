FROM jcolfej/steamcmd-rcon

LABEL maintainer="contact@colfej.fr"

# Steam
ENV GAME_STEAM_ID="376030" \
    GAME_INSTALL_DIR="/srv/ark/"

# RCON
ENV RCON_PORT="32330" \
    RCON_HEALTH_COMMAND="listplayers" \
    RCON_HEALTH_REGEXP="(No Players|[0-9]\.)" \
    RCON_GAME_LOG_BUFFER="100"

# Ark - Exec
ENV ARK_MAP="TheIsland" \
    ARK_MOD_LIST="" \
    ARK_BATTLE_EYE="true" \
    ARK_PORT="7777" \
    ARK_RAWPORT="7778" \
    ARK_QUERYPORT="27015" \
    ARK_MAX_PLAYERS="20"

# Expose ports
EXPOSE $ARK_PORT/udp $ARK_RAWPORT/udp $ARK_QUERYPORT/udp $RCON_PORT

# Workdir
WORKDIR /srv/ark/

# Add run script
ADD run.sh /srv/ark/run.sh
RUN chmod +x /srv/ark/run.sh

# Install ark-moddodo
RUN curl -Lo master.tar.gz https://github.com/xcq1/ark-moddodo/archive/master.tar.gz \
    && tar -xvzf /srv/ark/master.tar.gz \
    && rm /srv/ark/master.tar.gz

# Add signal to stop container
STOPSIGNAL SIGINT

# Set volume
VOLUME ["/srv/"]

# Exec run script
CMD /srv/ark/run.sh