FROM anapsix/alpine-java

WORKDIR /minecraft

RUN mkdir bin && wget -O bin/server.jar https://cdn.getbukkit.org/spigot/spigot-1.14.4.jar

COPY ./start.sh .

ENTRYPOINT ["./start.sh"]