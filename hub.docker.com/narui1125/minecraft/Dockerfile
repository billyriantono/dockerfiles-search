FROM ubuntu

MAINTAINER narui1125

EXPOSE 19132/udp

# 設定ファイル
VOLUME /config

# リソース
VOLUME /minecraft-server/behavior_packs
VOLUME /minecraft-server/resource_packs
VOLUME /minecraft-server/worlds

# 公式サーバーのダウンロードと展開
RUN apt-get update && apt-get install -y curl wget unzip && apt-get clean && rm -rf /var/lib/apt/lists/* \
  && wget -q -O minecraft-server.zip https://minecraft.azureedge.net/bin-linux/bedrock-server-1.10.0.7.zip \
  && unzip minecraft-server.zip -d minecraft-server \
  && rm -rf minecraft-server.zip

# シンボリックリンクの作成
RUN ln -sf /config/whitelist.json /minecraft-server/whitelist.json \
  && ln -sf /config/permissions.json /minecraft-server/permissions.json \
  && ln -sf /config/server.properties /minecraft-server/server.properties

WORKDIR minecraft-server

CMD LD_LIBRARY_PATH=. ./bedrock_server
