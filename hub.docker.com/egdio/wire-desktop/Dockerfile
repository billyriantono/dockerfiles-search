# Run Wire messenger (wire.com) in a container
#
# docker run -it \
#	-v /tmp/.X11-unix:/tmp/.X11-unix \ # mount the X11 socket
#       -v /etc/localtime:/etc/localtime:ro \
#       -v $HOME/.config/Wire:/home/signal/.config/Wire \
#	-e DISPLAY=unix$DISPLAY \
#	--device /dev/snd \ # so we have sound
#	--name wire \
#	egdio/wire-desktop

# Base docker image
FROM debian:sid-slim
LABEL maintainer "Ethan Gregory Dodge <ethan@egd.io>"

# Install depedencies, add Signal key and repo, install 
RUN apt update && apt install -y \
    curl \
    gnupg \
    libgtk-3-0 \
    libx11-xcb1 \
    && curl -s https://wire-app.wire.com/linux/releases.key | apt-key add - \
    && echo "deb https://wire-app.wire.com/linux/debian stable main" | tee -a /etc/apt/sources.list.d/wire-desktop.list \
    && apt update \
    && apt install -y wire-desktop \
    --no-install-recommends \
    && rm -rf /var/lib/apt/lists/*

# Add signal user
RUN groupadd -r wire && useradd -r -g wire -G audio,video wire \
    && mkdir /home/wire && chown -R wire:wire /home/wire

# Run as non privileged user
USER wire 

ENTRYPOINT [ "wire-desktop" ]
