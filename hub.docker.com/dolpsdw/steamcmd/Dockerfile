FROM i386/debian:buster-slim
# DockerFile debian 32 Steamcmd better compatibility at least on tf2

RUN apt update && apt install -y curl libcurl3-gnutls libtinfo5 && apt clean &&\
    mkdir /Steam && cd /Steam &&\
    echo $'#!/usr/bin/env bash\n\
if [ ! -f /Steam/steamcmd.sh ]; then\n\
    curl -sqL "https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz" | tar zxvf - -C /Steam\n\
    /Steam/steamcmd.sh +quit\n\
    ln -s /Steam/linux32 /root/.steam/sdk32\n\
    echo "Finished install" && bash\n\
fi' >> /Steam/firstTimeInstall.sh &&\
    chmod +x firstTimeInstall.sh
CMD /Steam/firstTimeInstall.sh
# VOLUME /DedServers # Not needed better practice is use Named Volumes.
# From here you can go into the container shell and start downloading and configure the servers.
# You can edit firstTimeInstall and handle the else to Auto Up your server when container is restarted.
# Remember map yor ports with run -p or use -network Host
