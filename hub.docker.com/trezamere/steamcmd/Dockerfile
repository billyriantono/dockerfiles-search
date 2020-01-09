############################################################
# Dockerfile that contains SteamCMD
############################################################
FROM debian:stretch-slim
LABEL maintainer="trezamere"

# Install, update & upgrade packages
# Create user for the server
# This also creates the home directory we later need
# Clean TMP, apt-get cache and other stuff to make the image smaller
# Create Directory for SteamCMD
# Download SteamCMD
# Extract and delete archive
RUN set -x \
	&& apt-get update \
	&& apt-get install -y --no-install-recommends --no-install-suggests \
		lib32gcc1 \
		wget \
		ca-certificates \
	&& useradd -m steam \
	&& su steam -c \
		"mkdir -p /home/steam/Steam \
		&& cd /home/steam/Steam \
		&& wget -qO- 'https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz' | tar zxf -" \
        && apt-get clean autoclean \
        && apt-get autoremove -y \
        && rm -rf /var/lib/{apt,dpkg,cache,log}/

WORKDIR /home/steam
CMD [ "/home/steam/Steam/steamcmd.sh" ]

# Switch to user steam
USER steam
