FROM        ubuntu:18.04


RUN         apt-get -y update && \
            apt-get -y --no-install-recommends install curl cron lib32gcc1 ca-certificates && \
            
            cd /tmp && \
            curl -sSL -o steamcmd.tar.gz http://media.steampowered.com/installer/steamcmd_linux.tar.gz && \

            mkdir -p /server/steamcmd && \
            tar -xzvf steamcmd.tar.gz -C /server/steamcmd && \
            
            mkdir -p /server/.steam/sdk32 && \
            # cp -v linux32/steamclient.so ../.steam/sdk32/steamclient.so && \
            chown -R root:root /server
  
            
COPY        ./server /server
