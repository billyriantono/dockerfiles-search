###########################################################
# Dockerfile that builds an ARK Gameserver
###########################################################
FROM cm2network/steamcmd

LABEL maintainer="skinlayers@gmail.com"

ENV STEAMCMDDIR /home/steam/steamcmd
ENV STEAMAPPID 376030
ENV STEAMAPPDIR /home/steam/ark

USER root

RUN apt update && apt -y install locales && \
    sed -i -e 's/^# \(en_US.UTF-8 UTF-8\)$/\1/' /etc/locale.gen && \
    locale-gen && \
    rm -rf /var/lib/{apt,dpkg,cache,log}/

USER steam

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

# Run Steamcmd and install ARK
RUN set -x \
	&& ${STEAMCMDDIR}/steamcmd.sh \
		+login anonymous \
		+force_install_dir ${STEAMAPPDIR} \
		+app_update ${STEAMAPPID} \
		+quit

ENV ARK_SESSION_NAME="ark_server"
ENV ARK_SERVER_PW="changeme"
ENV ARK_ADMIN_PW="changeme2"

WORKDIR $STEAMAPPDIR

VOLUME $STEAMAPPDIR

# Set Entrypoint:
# 1. Update server
# 2. Start server
ENTRYPOINT ${STEAMCMDDIR}/steamcmd.sh \
		+login anonymous +force_install_dir ${STEAMAPPDIR} +app_update ${STEAMAPPID} +quit \
		&& ${STEAMAPPDIR}/ShooterGame/Binaries/Linux/ShooterGameServer TheIsland?listen?SessionName=${ARK_SESSION_NAME}?ServerPassword=${ARK_SERVER_PW}?ServerAdminPassword=${ARK_ADMIN_PW} -server -log

# Expose ports
EXPOSE 7777/udp 7778/udp 27015/udp
