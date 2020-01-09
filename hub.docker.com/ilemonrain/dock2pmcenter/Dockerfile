# ####################################################
# o |                                   o     
# . |    ,---.,-.-.,---.,---.,---.,---. . ,---.
# | |    |---'| | ||   ||   ||    ,---| | |   |
# ` `---'`---'` ' '`---'`   '`    `---^ ` `   '
# ####################################################
#                                     __           
#     ____  ____ ___  ________  ____  / /____  _____
#    / __ \/ __ `__ \/ ___/ _ \/ __ \/ __/ _ \/ ___/
#   / /_/ / / / / / / /__/  __/ / / / /_/  __/ /    
#  / .___/_/ /_/ /_/\___/\___/_/ /_/\__/\___/_/     
# /_/             
#
# ####################################################
#
# PMCenter on Docker
#  -- A *Dockerized* telegram bot helping you to process private messages.
#
# Docker Image by: iLemonrain <ilemonrain@ilemonrain.com>
# Telegram Bot by: Elepover
# Docker Image Project: https://hub.docker.com/r/ilemonrain/pmcenter
# Telegram Bot Project: https://github.com/Elepover/pmcenter
#

FROM alpine:3.9

LABEL MAINTAINER="iLemonrain <ilemonrain@ilemonrain.com>" \
      VERSION="20190330"

COPY include/d2pmc /usr/bin/d2pmc

RUN ( apk update ;\
      # 安装基础环境
      apk add g++ gettext-dev git icu ;\
      # 安装 .Net Core + SDK
      mkdir -p /tmp/_lemonbuild/dotnet/ && cd /tmp/_lemonbuild/dotnet/ ;\
      wget -O /tmp/_lemonbuild/dotnet/dotnet-sdk.tar.gz https://download.visualstudio.microsoft.com/download/pr/f447ae7c-96d7-4a77-9e3a-fae23d67d4bb/71048b4741c1c5d531a40842b169d82e/dotnet-sdk-2.2.105-linux-musl-x64.tar.gz ;\
      tar xf dotnet-sdk.tar.gz ;\
      mkdir /usr/share/dotnet ;\
      cp -f /tmp/_lemonbuild/dotnet/dotnet /usr/share/dotnet/dotnet ;\
      cp -rf /tmp/_lemonbuild/dotnet/host/ /usr/share/dotnet/host/ ;\
      cp -rf /tmp/_lemonbuild/dotnet/shared/ /usr/share/dotnet/shared/ ;\
      cp -rf /tmp/_lemonbuild/dotnet/sdk/ /usr/share/dotnet/sdk/ ;\
      ln -s /usr/share/dotnet/dotnet /usr/bin/dotnet ;\
      chmod +x /usr/bin/dotnet ;\
      cd / && rm -rf /tmp_lemonbuild/dotnet ;\
      # 安装PMCenter
      mkdir -p /tmp/_lemonbuild/ && cd /tmp/_lemonbuild/ ;\
      git clone https://github.com/Elepover/pmcenter.git --depth=1 ;\
      cd /tmp/_lemonbuild/pmcenter/pmcenter ;\
      dotnet restore && dotnet publish --configuration Release ;\
      mkdir -p /usr/share/pmcenter/ ;\
      cp -rf /tmp/_lemonbuild/pmcenter/pmcenter/bin/Release/netcoreapp2.1/publish/* /usr/share/pmcenter/ ;\
      cd / && rm -rf tmp/_lemonbuild/pmcenter ;\
      # 配置权限
      chmod +x /usr/bin/d2pmc ;\
      # 卸载 .Net Core SDK
      rm -rf /usr/share/dotnet/sdk/ ;\
      # 卸载无关软件
      apk del git;\
      # 清理环境
      rm -rf /var/cache/apk/* /tmp/* ;\
)

CMD [ "sh" ]