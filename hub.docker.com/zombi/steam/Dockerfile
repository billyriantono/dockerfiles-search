FROM debian:stretch

ENV DEBIAN_FRONTEND noninteractive

# Create user steam
RUN useradd -m -d /home/steam steam

# Install dependencies (and goodies for mods)
RUN apt-get update &&\
    apt-get install -y curl lib32gcc1 lib32stdc++6 unzip git

# Download and extract SteamCMD
RUN mkdir -p /opt/steamcmd &&\
    cd /opt/steamcmd &&\
    curl -s http://media.steampowered.com/installer/steamcmd_linux.tar.gz | tar -vxz

WORKDIR /opt/steamcmd

# update steam
RUN ./steamcmd.sh +quit
