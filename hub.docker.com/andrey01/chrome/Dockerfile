# Run Chrome in a container
FROM ubuntu:zesty
MAINTAINER Andrey Arapov <andrey.arapov@nixaid.com>

# To avoid problems with Dialog and curses wizards
ENV DEBIAN_FRONTEND noninteractive

# Install GTK, pulseaudio and fonts
RUN apt-get update && \
    apt-get -y --no-install-recommends install ca-certificates tzdata \
                       libcanberra-gtk-module libexif12 pulseaudio attr \
                       fonts-dejavu-core fonts-freefont-ttf fonts-guru-extra \
                       fonts-kacst fonts-kacst-one fonts-khmeros-core fonts-lao \
                       fonts-liberation fonts-lklug-sinhala fonts-lohit-guru \
                       fonts-nanum fonts-opensymbol fonts-sil-abyssinica \
                       fonts-sil-padauk fonts-symbola fonts-takao-pgothic \
                       fonts-tibetan-machine fonts-tlwg-garuda-ttf \
                       fonts-tlwg-kinnari-ttf fonts-tlwg-laksaman-ttf \
                       fonts-tlwg-loma-ttf fonts-tlwg-mono-ttf \
                       fonts-tlwg-norasi-ttf fonts-tlwg-purisa-ttf \
                       fonts-tlwg-sawasdee-ttf fonts-tlwg-typewriter-ttf \
                       fonts-tlwg-typist-ttf fonts-tlwg-typo-ttf \
                       fonts-tlwg-umpush-ttf fonts-tlwg-waree-ttf \
                       ttf-bitstream-vera ttf-dejavu-core ttf-ubuntu-font-family \
                       fonts-arphic-ukai fonts-arphic-uming \
                       fonts-ipafont-mincho fonts-ipafont-gothic \
                       fonts-unfonts-core && \
    rm -rf -- /var/lib/apt/lists /tmp/*.deb

# Obtain Google Chrome
ADD https://dl.google.com/linux/direct/google-talkplugin_current_amd64.deb /tmp/google-talkplugin_current_amd64.deb
ADD https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb /tmp/google-chrome-stable_current_amd64.deb

# Install Google Chrome and its dependencies
RUN sh -c 'dpkg -i /tmp/google-chrome-stable_current_amd64.deb \
           /tmp/google-talkplugin_current_amd64.deb 2>/dev/null; exit 0' && \
    apt-get update && \
    apt-get -fy install && \
    rm -rf -- /var/lib/apt/lists /tmp/*.deb

# Workaround: pulseaudio client library likes to remove /dev/shm/pulse-shm-*
#             files created by the host, causing sound to stop working.
#             To fix this, we either want to disable the shm or mount /dev/shm
#             in read-only mode when starting the container.
RUN echo "enable-shm = no" >> /etc/pulse/client.conf

ENV USER user
ENV GROUPS video,audio
ENV UID 1000
ENV HOME /home/$USER

RUN useradd -u $UID -m -d $HOME -s /usr/sbin/nologin -G $GROUPS $USER && \
    su -s /bin/sh -l $USER -c 'mkdir -p $HOME/.pki/nssdb $HOME/.local'

WORKDIR $HOME

COPY launch /launch
ENTRYPOINT [ "sh", "/launch" ]
