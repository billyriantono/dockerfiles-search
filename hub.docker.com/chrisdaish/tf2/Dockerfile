FROM chrisdaish/steamcmd

MAINTAINER Chris Daish <chrisdaish@gmail.com>

USER steam

WORKDIR /home/steam

RUN /home/steam/steamcmd.sh \
      +login anonymous \
      +force_install_dir tf2 \
      +app_update 232250 validate \
      +quit

EXPOSE 27015

WORKDIR /home/steam/steamcmd/tf2

ENTRYPOINT ["/home/steam/tf2/srcds_run"]
