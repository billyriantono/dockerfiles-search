#
# This is unofficial dockerized precompiled AdGuardHome within a debian:stable-slim image.
#

FROM arm32v7/debian:stretch-slim 
COPY qemu-arm-static /usr/bin

COPY AdGuardHome.yaml /AdGuardHome.yaml
COPY start_agh.sh /start_agh.sh

RUN export DEBIAN_FRONTEND=noninteractive \
&& export URL=https://api.github.com/repos/AdguardTeam/AdGuardHome/releases/latest \
&& export OS="linux" \
&& apt-get update && apt-get upgrade -y \
&& apt-get install --no-install-recommends -y ca-certificates wget curl \
&& cd /opt \
&& wget --tries=3 https://github.com/AdguardTeam/AdGuardHome/releases/download/v0.96-hotfix/AdGuardHome_linux_arm.tar.gz \
&& tar -xvzf *.tar.gz \
&& rm *.tar.gz \
&& mkdir /opt/AdGuardHome/config \
&& chmod a+rx /start_agh.sh \
&& apt-get purge -y -q --auto-remove wget curl \
&& apt-get clean \
&& cd / \
&& rm -rf /var/lib/apt/lists/* /var/tmp/* /tmp/*

VOLUME [ "/opt/AdGuardHome/config" ]

EXPOSE 53/udp 3000

ENTRYPOINT ["/start_agh.sh"]
