FROM ubuntu:18.04
# setup directory where user data is stored
VOLUME ["/home/ts3/data/"]
WORKDIR /home/ts3/data/
ENV TEAMSPEAK_URL https://www.dropbox.com/s/c1dlhjblg5e1n36/teamspeak3-server_linux_amd64.tar.gz
ENV TS3_UID 1000
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
RUN apt-get update -q \
  && DEBIAN_FRONTEND=noninteractive apt-get install -qy bzip2 wget \
  && apt-get clean \
  && rm -rf /var/lib/apt \
  && useradd -u ${TS3_UID} ts3 \
  && mkdir -p /home/ts3 \
  && wget -q -O /home/ts3/teamspeak3-server_linux_amd64.tar.gz ${TEAMSPEAK_URL} \
  && tar xfz /home/ts3/teamspeak3-server_linux_amd64.tar.gz -C /home/ts3 \
  && rm /home/ts3/teamspeak3-server_linux_amd64.tar.gz \
  && mkdir -p /home/ts3/data/logs \
  && mkdir -p /home/ts3/data/files \
  && ln -s /home/ts3/data/files /home/ts3/teamspeak3-server_linux_amd64 \
  && ln -s /home/ts3/data/ts3server.sqlitedb /home/ts3/teamspeak3-server_linux_amd64/ts3server.sqlitedb \
  && chown -R ts3 /home/ts3
ENV PATH "${PATH}:/home/ts3/teamspeak3-server_linux_amd64"
# 9987 default voice
# 1365 custom voice
# 10011 server query
# 30033 file transport
EXPOSE 1365/udp 10011 30033
# ENTRYPOINT [ "/home/ts3/teamspeak3-server_linux_amd64/ts3server_minimal_runscript.sh","/home/ts3/teamspeak3-server_linux_amd64/AccountingServerEmulator-Linux" ]
COPY entrypoint.sh /home/ts3/teamspeak3-server_linux_amd64
RUN chmod +x /home/ts3/teamspeak3-server_linux_amd64/entrypoint.sh
ENTRYPOINT [ "entrypoint.sh","AccountingServerEmulator-Linux" ]
CMD [ "ts3server" ]
