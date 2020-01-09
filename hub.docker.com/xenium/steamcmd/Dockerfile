FROM ubuntu
MAINTAINER Frenzoid <frenzoid@protonmail.com>

ENV VOL /root/steam
ENV STEAMCMDDIR ${VOL}/steamcmd
ENV GAMEDIR ${VOL}/game

COPY start.sh /root/steam/steamcmd/start.sh

RUN apt-get update 
RUN apt-get update                      &&      \
    apt-get upgrade -y                  &&      \
    apt-get install -y                          \
        curl                                    \
        lib32gcc1				\
	lib32tinfo5				\
	libncurses5				\
	libncurses5			\
	libc6				\
	libstdc++6				\
	lib32z1					\
	libcurl3-gnutls			\
	curl
		
RUN mkdir -p ${STEAMCMDDIR} ${GAMEDIR} \
	&& cd ${STEAMCMDDIR} \
	&& curl -s 'https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz' | tar -vxz -C /root/steam/steamcmd/
	
RUN apt-get clean autoclean
RUN apt-get autoremove -y

RUN rm -rf /var/lib/apt/lists/*
RUN chmod +x /root/steam/steamcmd/start.sh

VOLUME $VOL

WORKDIR $STEAMCMDDIR
ENTRYPOINT ["/bin/bash", "-c", "./start.sh"]
