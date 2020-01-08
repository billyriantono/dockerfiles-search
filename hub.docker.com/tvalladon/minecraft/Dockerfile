# -----------------------------------------------------------------------------
# docker-minecraft
#
# Builds a basic docker image that can run a Minecraft server
# (http://minecraft.net/).
#
# Authors: Terry Valladon
# Updated: July 6th, 2014
# Require: Docker (http://www.docker.io/)
# -----------------------------------------------------------------------------


# Base system is the LTS version of Ubuntu.
from tvalladon/openjdk7 

expose 25565
volume ["/data"]
workdir /data
cmd /bin/sh LaunchServer.sh >> /logs/$HOSTNAME-`date "+%Y-%m-%d"`.log
