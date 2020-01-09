FROM sovich/srcdsrun-base:latest

ENV SERVER /server
ENV CACHE_DIR /path/servers/cssold/default/

RUN mkdir -p $CACHE_DIR \
    && cd $CACHE_DIR \
    && curl -s http://shara.cw-serv.ru/servers/cssold/default.tar.gz | tar xzv hl2/ platform/

WORKDIR $SERVER

ENTRYPOINT ["./srcds_run"]
CMD ["-game", "cstrike", "-nomaster", "-localcser", "+map", "de_dust2", "+maxplayers", "10", "-port", "27015", "-ip", "0.0.0.0"]
