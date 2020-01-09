FROM ubuntu:xenial

MAINTAINER ingildsens (https://github.com/ingildsens)

RUN \

# install packages
apt-get update && \
apt-get install -y \
encfs \
python3-appdirs \
python3-colorama \
python3-dateutil \
python3-requests \
python3-sqlalchemy \
python3-pip \
git \
unionfs-fuse \
nano \
wget && \

# setup file structure
mkdir -p \
/home/plex/.local-sorted/ \
/home/plex/local-sorted/ \
/home/plex/.acd-sorted/ \
/home/plex/acd-sorted/ \
/home/plex/sorted/ \
~/.cache/acd_cli/ && \

# create oauth_data
touch ~/.cache/acd_cli/oauth_data && \

# install acd_cli
pip3 install --upgrade git+https://github.com/yadayada/acd_cli.git && \

# install plex
wget -P ~/ https://downloads.plex.tv/plex-media-server/1.2.5.2966-3f767e7/plexmediaserver_1.2.5.2966-3f767e7_amd64.deb && \
dpkg -i ~/plexmediaserver_1.2.5.2966-3f767e7_amd64.deb && \

# cleanup
apt-get clean && \
rm -rf \
/tmp/* \
/var/lib/apt/lists/* \
/var/tmp/* 

# keep running
ENTRYPOINT ["/bin/bash"]
