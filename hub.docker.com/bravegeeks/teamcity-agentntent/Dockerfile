############################################################
# Dockerfile that builds a Post Scriptum Gameserver
############################################################
FROM cm2network/steamcmd
LABEL maintainer="brainp4in@blueberry-hood-clan.de"

# Run Steamcmd and install Squad
RUN ./home/steam/steamcmd/steamcmd.sh +login anonymous \
        +force_install_dir /home/steam/post-scriptum-dedicated \
        +app_update 746200 validate \
        +quit

ENV PORT=10027 QUERYPORT=10037 RCONPORT=21114 FIXEDMAXPLAYERS=80 RANDOM=NONE TASKSET="0-7"

VOLUME /home/steam/post-scriptum-dedicated

# Set Entrypoint; Technically 2 steps: 1. Update server, 2. Start server
ENTRYPOINT /home/steam/steamcmd/steamcmd.sh +login anonymous +force_install_dir /home/steam/post-scriptum-dedicated +app_update 746200 +quit && \
        cd /home/steam/post-scriptum-dedicated/; taskset -c $TASKSET /home/steam/post-scriptum-dedicated/PostScriptumServer.sh Port=$PORT QueryPort=$QUERYPORT RCONPORT=$RCONPORT FIXEDMAXPLAYERS=$FIXEDMAXPLAYERS RANDOM=$RANDOM
        
# Expose ports
EXPOSE 10027 10037 21114
