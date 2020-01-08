ARG linux_base=ubuntu:bionic
ARG node_version=10.16.3
ARG downloader_image=fczuardi/node_download

# image containing downloaded binaries
FROM ${downloader_image}:${node_version} as download

FROM ${linux_base}
WORKDIR "/opt/node"
COPY --from=download /opt/node .
ENV PATH=$PATH:/opt/node/bin
