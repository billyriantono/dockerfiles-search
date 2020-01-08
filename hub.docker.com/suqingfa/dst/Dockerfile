FROM wilkesystems/steamcmd

MAINTAINER su <enmoton@qq.com>

EXPOSE 10999 10888

VOLUME ["/dst/mods","/root/.klei/DoNotStarveTogether/Server/"]

RUN apt-get update && \
  apt-get install -y libcurl4-gnutls-dev:i386 && \
  apt-get clean

RUN steamcmd +login anonymous +force_install_dir /dst +app_update 343050 validate +quit

ADD entrypoint /
RUN chmod +x /entrypoint

ENTRYPOINT ["/entrypoint"]
