FROM ubuntu:bionic

LABEL maintainer="contact@colfej.fr"

# Language
ENV LC_ALL=C.UTF-8 \
    LANG=en_US.UTF-8 \
    LANGUAGE=en_US.UTF-8

# Steam
ENV GAME_STEAM_ID="000000" \
    GAME_INSTALL_DIR="/srv/game/"

# Install gcc, curl and mc
RUN apt update \
    && apt install -y lib32gcc1 curl mc \
    && apt clean \
    && rm -rf /var/lib/apt/lists/*

# Set workdir
WORKDIR /srv/steam

# Add install script
ADD install.sh /srv/steam/
RUN chmod +x /srv/steam/install.sh

# Add SteamCMD installer
RUN curl -sqL "https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz" | tar zxvf -

# Exec install script
CMD /srv/steam/install.sh