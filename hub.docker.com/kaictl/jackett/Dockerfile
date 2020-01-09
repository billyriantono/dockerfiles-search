FROM ubuntu:18.04

ARG DEBIAN_FRONTEND="noninteractive"
ENV XDG_DATA_HOME="/config" \
XDG_CONFIG_HOME="/config"

RUN apt-get update
RUN apt-get install -y --no-install-recommends libicu60 libssl1.0 ca-certificates curl jq

RUN mkdir -p /Jackett && \
    JACKETT_RELEASE=$(curl -ksX GET "https://api.github.com/repos/Jackett/Jackett/releases/latest" \
    | jq -r .tag_name); \
    curl -kL "https://github.com/Jackett/Jackett/releases/download/${JACKETT_RELEASE}/Jackett.Binaries.LinuxAMDx64.tar.gz" \
    | tar -xz -C /Jackett --strip-components=1
RUN apt-get autoremove -y curl jq && apt-get clean

RUN mkdir -pv /jackett /config /downloads && \
    chown -R 1000:1000 /jackett /config /downloads

RUN rm -rf /var/lib/apt/lists/*

VOLUME /config /downloads
EXPOSE 9117

USER 1000:1000
CMD ["/Jackett/jackett", "--NoRestart"]