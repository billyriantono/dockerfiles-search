FROM archlinux/base
LABEL maintainer "Adam Bozson <adam@bozson.io>"

COPY pacman.conf /etc/pacman.conf
RUN pacman -Syu --noconfirm
RUN pacman -S --noconfirm wget file nvidia nvidia-utils lib32-nvidia-utils mesa-demos ttf-liberation xdg-user-dirs pciutils base-devel --needed
RUN pacman -S --noconfirm steam 

RUN pacman -S --noconfirm pulseaudio pulseaudio-alsa lib32-libpulse lib32-alsa-plugins
COPY pulseaudio.client.conf /etc/pulse/client.conf
ENV PULSE_SERVER=/tmp/pulseaudio.socket PULSE_COOKIE=/tmp/pulseaudio.cookie

COPY machine-id /etc/machine-id

RUN groupadd -g 1000 steam-user \ 
    && useradd --no-log-init -rm -u 1000 -g 1000 steam-user
USER steam-user
ENV LANG en-GB

CMD ["steam"]
