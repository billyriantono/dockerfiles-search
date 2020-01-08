# This file describes the standard way to build Docker, using docker
#
# Usage:
#
# # Assemble the full dev environment. This is slow the first time.
# docker build -t docker .
#

docker-version	0.9.0
FROM	jack/ubuntubase:ssh
MAINTAINER	Jack Li<jack.qingtian@gmail.com>

# Add an unprivileged user to be used for tests which need it
RUN groupadd -r docker
RUN useradd --create-home --gid docker docker
