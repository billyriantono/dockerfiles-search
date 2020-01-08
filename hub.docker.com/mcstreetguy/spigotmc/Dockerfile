# Build Stage for Server
FROM openjdk:8-alpine as build_server
WORKDIR /tmp

RUN apk add --no-cache bash curl git && \
    curl -O https://hub.spigotmc.org/jenkins/job/BuildTools/lastSuccessfulBuild/artifact/target/BuildTools.jar

ARG version=1.14.4
ENV VERSION=${version}

RUN java -jar ./BuildTools.jar --rev ${VERSION} --output-dir /tmp && \
    mv /tmp/spigot-${VERSION}.jar /tmp/spigot.jar

# Build Stage for RCON
FROM alpine:3.10 as build_rcon
WORKDIR /tmp

RUN apk add --no-cache bash git g++ make

RUN git clone https://github.com/Tiiffi/mcrcon.git mcrcon && \
    cd mcrcon && \
    make && \
    chmod +x mcrcon

# Build Stage for init system
FROM alpine:3.10 as initsystem

ADD https://github.com/just-containers/s6-overlay/releases/download/v1.21.8.0/s6-overlay-amd64.tar.gz /tmp/
RUN apk add --no-cache tar && \
    mkdir -p /opt/s6-overlay/ && \
    tar xzf /tmp/s6-overlay-amd64.tar.gz -C /opt/s6-overlay/

# Main Stage
FROM alpine:3.10

RUN mkdir -p /etc/cont-init.d/ /etc/fix-attrs.d/ /etc/services.d/
RUN apk add --no-cache bash openjdk8

COPY --from=initsystem /opt/s6-overlay/ /
COPY --from=build_server /tmp/spigot.jar /tmp/minecraft/bin/
COPY --from=build_rcon /tmp/mcrcon/mcrcon /usr/local/bin/mcrcon
COPY ./service/ /etc/
COPY ./server/ /tmp/minecraft/
COPY ./bin/ /usr/local/bin/

WORKDIR /opt/minecraft/

VOLUME [ "/opt/minecraft/" ]

EXPOSE 25565
EXPOSE 25575

ENTRYPOINT [ "/init" ]
