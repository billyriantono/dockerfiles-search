FROM chrisdaish/steamcmd

MAINTAINER Chris Daish <chrisdaish@gmail.com>

USER steam

WORKDIR /home/steam

RUN /home/steam/steamcmd.sh \
      +login anonymous \
      +force_install_dir csgo \
      +app_update 740 validate \
      +quit

EXPOSE 27015

WORKDIR /home/steam/steamcmd/csgo

ENTRYPOINT ["/home/steam/steamcmd/csgo/srcds_run"]
