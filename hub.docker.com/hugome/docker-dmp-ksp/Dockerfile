FROM hugome/docker-dmp-ksp

WORKDIR /DMPServer/Plugins/

RUN apt-get update && \
    apt-get install -y wget && \
    wget http://godarklight.info.tm/dmp/downloads/plugins/DMPServerListReporter2/DMPServerListReporter.dll && \
    apt-get remove -y --purge wget && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /
