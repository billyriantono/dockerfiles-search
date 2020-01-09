FROM longshot902/docker-steamcmd

MAINTAINER Jeff Nelson <longshot902@gmail.com>

## Create Environment Variables
## Game Specific
ENV GAME="tf" STEAM_APP="232250" STEAMCMD_USER="anonymous" STEAMCMD_PASSWORD="" STEAMCMD_AUTH_CODE=""

## Steam Specific
ENV USER="steam" SERVER_DIRECTORY="/home/steam/" GAME_DIRECTORY="/home/steam/tf/"

## Add files
ADD start.sh $GAME_DIRECTORY/

## Assign user permissions
USER $USER
RUN sudo chmod u+x -R $SERVER_DIRECTORY $GAME_DIRECTORY \
    && sudo chown $USER:$USER -R $SERVER_DIRECTORY $GAME_DIRECTORY

## Update to latest TF2
RUN $SERVER_DIRECTORY/steamcmd.sh +login $STEAMCMD_USER $STEAMCMD_PASSWORD $STEAMCMD_AUTH_CODE +force_install_dir $GAME_DIRECTORY +app_update $STEAM_APP +quit

## Open default ports
EXPOSE 27015/udp

## Set working directory and normal start up process
WORKDIR $GAME_DIRECTORY
ENTRYPOINT ["./start.sh"]
CMD ["+map", "ctf_2fort", "+maxplayers", "24"]