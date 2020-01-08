FROM marthym/base:1.3.0
LABEL maintainer="marthym@ght1pc9kc.fr"

ENV NODE_VERSION=10.4.1 \
    NGCLI_VERSION=6.0.2 \
    CHROME_BIN=chromium

RUN export DEBIAN_FRONTEND=noninteractive && \
    apt update && \
    apt install -y --no-install-recommends ca-certificates xz-utils git chromium && \
    #
    curl "https://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-x64.tar.xz" --output "node-v${NODE_VERSION}-linux-x64.tar.xz" && \
    tar xJf node-v${NODE_VERSION}-linux-x64.tar.xz -C /opt && \
    ln -s /opt/node-v${NODE_VERSION}-linux-x64/bin/node /usr/local/bin/node && \
    ln -s /opt/node-v${NODE_VERSION}-linux-x64/bin/npm /usr/local/bin/npm && \
    npm --global install @angular/cli@${NGCLI_VERSION} --unsafe-perm=true --allow-root && \
    ln -s /opt/node-v${NODE_VERSION}-linux-x64/bin/ng /usr/local/bin/ng && \
    ng --version && \
    #
    apt purge -y wget ca-certificates xz-utils && \
    apt autoremove -y && \
    apt clean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /tmp/*
