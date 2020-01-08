FROM openjdk:8

WORKDIR /opt/minecraft

ADD https://media.forgecdn.net/files/2524/140/FTBPresentsDirewolf20112Server.zip .
COPY configs .

RUN unzip FTBPresentsDirewolf20112Server.zip && rm FTBPresentsDirewolf20112Server.zip && \
            chmod +x /opt/minecraft/ServerStart.sh

EXPOSE 25565
VOLUME [ "/opt/minecraft" ]
ENTRYPOINT [ "/opt/minecraft/ServerStart.sh" ]