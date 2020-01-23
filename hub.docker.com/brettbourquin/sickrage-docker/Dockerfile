#
# SiCKRAGE Dockerfile
#
# https://git.sickrage.ca/sickrage/sickrage-docker
#

FROM python:2

MAINTAINER echel0n <echel0n@sickrage.ca>

# Volumes and Ports
VOLUME /config /downloads /tv
EXPOSE 8081

# entrypoint
ADD docker-entrypoint.sh /
ENTRYPOINT ["/bin/sh", "/docker-entrypoint.sh", "--datadir=/config", "--nolaunch"]
