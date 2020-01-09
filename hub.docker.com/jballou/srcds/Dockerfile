FROM jballou/steamcmd

MAINTAINER Jared Ballou <github@jballou.com>
# Download and extract SteamCMD
#USER steam
WORKDIR /opt/steamcmd

RUN cd /opt/steamcmd && \
	./steamcmd.sh \
        +login anonymous \
        +app_update 740 validate \
        +quit

#        +force_install_dir ../csgo \
# Make server port available to host
EXPOSE 27015

# This container will be executable
#WORKDIR /home/steam/csgo
#ENTRYPOINT ["./srcds_run"]
