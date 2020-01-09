FROM cm2network/steamcmd
LABEL maintainer="chrisbloemendaal@gmail.com"

ENV GAME=garrysmod TICKRATE=66 MAXPLAYERS=16 GAMEMODE=required WORKSHOP=required AUTHKEY=required

ENTRYPOINT ./home/steam/steamcmd/steamcmd.sh +login anonymous +force_install_dir /home/steam/gmod-dedicated +app_update 4020 +app_update 232330 +quit && \
            ./home/steam/gmod-dedicated/srcds_run -console -debug -game $GAME -tickrate $TICKRATE -maxplayers $MAXPLAYERS +gamemode $GAMEMODE +host_workshop_collection $WORKSHOP -authkey $AUTHKEY

# Expose ports
EXPOSE 27015/tcp 27015/udp 27020/udp 27005/udp 26900/udp
