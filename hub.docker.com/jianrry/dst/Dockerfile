FROM ubuntu:latest

MAINTAINER Jianrry <jianrry@gmail.com>

RUN set -x \
        && dpkg --add-architecture i386 \
        && apt update \
        && apt-get install -y --no-install-recommends --no-install-suggests lib32gcc1 lib32stdc++6 libcurl4-gnutls-dev:i386 wget ca-certificates unzip \
        && mkdir -p /root/steamcmd \
        && cd /root/steamcmd \
        && wget https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz \
        && tar zxvf steamcmd_linux.tar.gz \
        && mkdir -p /root/.klei/DoNotStarveTogether \
        && cd /root/.klei/DoNotStarveTogether \
        && wget https://github.com/jianrry/dst/raw/master/MyDediServer.zip \
        && unzip MyDediServer.zip \
	&& cd /root/steamcmd \
	&& ./steamcmd.sh +login anonymous +force_install_dir /root/dst +app_update 343050 +quit \
	&& echo "ServerModSetup(\"1938752683\")" > /root/dst/mods/dedicated_server_mods_setup.lua \
        && cd /root/.klei/DoNotStarveTogether/MyDediServer \
        && wget https://raw.githubusercontent.com/jianrry/dst/master/run.sh \
        && chmod +x run.sh \
        && apt-get remove --purge -y wget ca-certificates unzip \
        && apt-get clean autoclean \
	&& apt-get autoremove -y \
	&& rm -rf /var/lib/apt/lists/*

CMD ["sh", "/root/.klei/DoNotStarveTogether/MyDediServer/run.sh"]

EXPOSE 10999/udp




