FROM ubuntu:wily
MAINTAINER Dave O Connor <docker@mail.andvari.net>

ENV DEBIAN_FRONTEND="noninteractive"

# Should be the same UID on the host.
RUN useradd --system --uid 2002 -M --shell /usr/bin/nologin media

# Update everything, because.
RUN echo "deb http://archive.ubuntu.com/ubuntu wily multiverse" >> /etc/apt/sources.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv-keys FDA5DFFC
RUN echo "deb http://apt.sonarr.tv/ master main" | tee /etc/apt/sources.list.d/sonarr.list
RUN apt-get -q update && apt-get -qy --force-yes dist-upgrade

RUN apt-get install -qy nzbdrone

USER media

# Sonarr stores everything in $HOME/.config
VOLUME [ "/home/media", "/data", "/media" ]

CMD [ "mono", "--debug", "/opt/NzbDrone/NzbDrone.exe" ]
