FROM centos:7
LABEL maintainer="Andrea Togni <togniand@gmail.com>"

ENV SOFTETHER_VERSION="latest"

RUN adduser -D -g softether -G softether -s /sbin/nologin ; \
    yum install -y curl make gcc; \
    mkdir -p /etc/vpnserver /var/log/vpnserver; \
    cd / ; \
    if [[ "x$SOFTETHER_VERSION" == "xlatest" ]]; then \
        curl -L -o vpnserver.tar.gz $(curl -s https://api.github.com/repos/SoftEtherVPN/SoftEtherVPN_Stable/releases | grep browser_download_url | grep softether-vpnserver | grep linux-x64-64bit | head -n 1 | cut -d '"' -f 4); \
    else \
        curl -L -o vpnserver.tar.gz $(curl -s https://api.github.com/repos/SoftEtherVPN/SoftEtherVPN_Stable/releases | grep browser_download_url | grep softether-vpnserver | grep linux-x64-64bit | grep "$SOFTETHER_VERSION" | cut -d '"' -f 4); \
    fi; \
    tar zxvf vpnserver.tar.gz; \
    rm -rf vpnserver.tar.gz; \
    cd vpnserver/ ; \
    make i_read_and_agree_the_license_agreement; \
    chown -R softether /vpnserver; \
    setcap 'cap_net_bind_service=+ep' /vpnserver/vpnserver

USER softether
WORKDIR /vpnserver


EXPOSE 443/tcp 992/tcp 1194/udp 5555/tcp 1701/udp 500/udp 4500/udp

VOLUME ["/etc/vpnserver", "/var/log/vpnserver"]

CMD ["./vpnserver", "start"]

