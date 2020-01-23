FROM execpcs/steam

MAINTAINER ExecPcs
ENV VERSION 1.1

USER root

# Prepare directory
RUN mkdir /opt/csgo &&\
    chown steam:steam /opt/csgo

# Run commands as the steam user
USER steam

# Install CS:GO
RUN /opt/steamcmd/steamcmd.sh \
        +login anonymous \
        +force_install_dir /opt/csgo \
        +app_update 740 validate \
        +quit

# Make server port available to host
EXPOSE 27015

# This container will be executable
WORKDIR /opt/csgo
ENTRYPOINT ["./srcds_run"]
