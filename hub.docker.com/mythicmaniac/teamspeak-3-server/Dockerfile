FROM debian:stretch-slim

ENV TS_VERSION LATEST
ENV LANG C.UTF-8

RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get -y install bzip2 wget ca-certificates \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /home/teamspeak3

RUN wget https://files.teamspeak-services.com/releases/server/3.7.1/teamspeak3-server_linux_amd64-3.7.1.tar.bz2 && \
    tar xvf teamspeak3-server_linux_amd64-3.7.1.tar.bz2 && \
    rm teamspeak3-server_linux_amd64-3.7.1.tar.bz2 && \
    cd teamspeak3-server_linux_amd64 && \
    touch .ts3server_license_accepted && \
    exit && \
    chown teamspeak3:teamspeak3 /home/teamspeak3

COPY start.sh /home/teamspeak3/.
RUN chmod +x /home/teamspeak3/start.sh

EXPOSE 9987/udp 10011 30033
CMD ["sh", "start.sh"]
