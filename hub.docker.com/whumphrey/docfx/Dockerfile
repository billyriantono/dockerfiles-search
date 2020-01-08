FROM mono:latest

LABEL maintainer="Wayne Humphrey <wayne@humphrey.za.net>" \
      description="Building documentation in docker with DocFX" \
      version="1.0"

ENV FX_VER 2.40.6
ENV DOC_REPO https://github.com/nitr8/docfx-sample.git

RUN apt-get update && apt-get install unzip wget git nginx --no-install-recommends -y && \
    wget -q -P /tmp https://github.com/dotnet/docfx/releases/download/v${FX_VER}/docfx.zip && \
    mkdir -p /opt/docfx && \
    unzip /tmp/docfx.zip -d /opt/docfx && \
    echo '#!/bin/bash\nmono /opt/docfx/docfx.exe $@' > /usr/bin/docfx && \
    chmod +x /usr/bin/docfx && \
    rm -f /tmp/* && \
    printf '#!/bin/sh \nnginx \ndocfx /docs/docfx.json --serve -p 8081' > /init  && \
    chmod +x /init && \
    git clone ${DOC_REPO} /docs

COPY nginx.conf /etc/nginx/nginx.conf

EXPOSE 8082
VOLUME  ["/docs"]

ENTRYPOINT ["/init"]
