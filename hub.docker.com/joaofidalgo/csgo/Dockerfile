FROM joaofidalgo/steamcmd

MAINTAINER João Fidalgo <joao.fidalgo@outlook.com>

RUN mkdir -p /opt/csgo

RUN /opt/steamcmd/steamcmd.sh \
    +login anonymous \
    +force_install_dir /opt/csgo \
    +app_update 740 validate \
    +quit

ONBUILD COPY ./cfg/*.cfg /opt/csgo/cfg

VOLUME /opt/csgo

EXPOSE 27015

CMD ["run"]
ENTRYPOINT ["/opt/csgo/srcds_run"]