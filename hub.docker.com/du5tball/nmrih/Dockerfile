FROM centos

RUN yum install -y sudo glibc.i686 libstdc++.i686 && \
    mkdir /steam && \
    curl http://media.steampowered.com/client/steamcmd_linux.tar.gz -o /steam/steamcmd_linux.tar.gz && \
    tar -xvzf /steam/steamcmd_linux.tar.gz -C /steam/

RUN /steam/steamcmd.sh +login anonymous +app_update 317670 validate +quit

RUN ln -s '/root/Steam/steamapps/common/No More Room in Hell Dedicated Server/bin/soundemittersystem_srv.so' \
          '/root/Steam/steamapps/common/No More Room in Hell Dedicated Server/bin/soundemittersystem.so' && \
    ln -s '/root/Steam/steamapps/common/No More Room in Hell Dedicated Server/bin/scenefilecache_srv.so' \
          '/root/Steam/steamapps/common/No More Room in Hell Dedicated Server/bin/scenefilecache.so'

EXPOSE 27015/tcp
EXPOSE 26901/udp
EXPOSE 27005/udp
EXPOSE 27015/udp
EXPOSE 27020/udp

ENTRYPOINT ["/root/Steam/steamapps/common/No More Room in Hell Dedicated Server/srcds_run", "-game", "nmrih", "-insecure", "-maxplayers", "8", "+map nmo_broadway"]

