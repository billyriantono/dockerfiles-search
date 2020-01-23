FROM ubuntu:xenial
MAINTAINER Andrey Arapov <andrey.arapov@nixaid.com>

# To avoid problems with Dialog and curses wizards
ENV DEBIAN_FRONTEND noninteractive

# Keep the image updated and install the dependencies
RUN apt-get update && \
    apt-get -y upgrade && \
    apt-get -y dist-upgrade && \
    apt-get -fy install && \
    apt-get -y install xz-utils libdbus-glib-1-2 libgtk2.0-0 libxt6 \
                       libgl1-mesa-glx pulseaudio attr && \
    rm -rf /var/lib/apt/lists

# bzip2 libgtk-3-0 libasound2 libpango1.0-0 libv4l-0 libgl1-mesa-glx x264

# Workaround: pulseaudio client library likes to remove /dev/shm/pulse-shm-*
#             files created by the host, causing sound to stop working.
#             To fix this, we either want to disable the shm or mount /dev/shm
#             in read-only mode when starting the container.
RUN echo "enable-shm = no" >> /etc/pulse/client.conf


ENV USER user
ENV UID 1000
ENV GROUPS video,audio
ENV HOME /home/$USER
RUN useradd -u $UID -m -d $HOME -s /usr/sbin/nologin -G $GROUPS $USER

ENV TORVER 7.0.5
ENV TORKEY "EF6E286DDA85EA2A4BA7DE684E2C6E8793298290"
ADD https://www.torproject.org/dist/torbrowser/${TORVER}/tor-browser-linux64-${TORVER}_en-US.tar.xz /tmp/tor.tar.xz
ADD https://www.torproject.org/dist/torbrowser/${TORVER}/tor-browser-linux64-${TORVER}_en-US.tar.xz.asc /tmp/tor.tar.xz.asc

RUN cd /tmp && \
    gpg --keyserver ha.pool.sks-keyservers.net --recv-keys $TORKEY && \
    gpg --verify tor.tar.xz.asc && \
    tar xf tor.tar.xz -C $HOME && \
    rm -f tor.tar.xz && \
    chown -Rh $USER:$USER $HOME

WORKDIR $HOME

VOLUME [ "/tmp", "$HOME/tor-browser" ]

COPY ./launch /launch
ENTRYPOINT [ "/bin/bash", "/launch" ]
