FROM debian:wheezy
RUN DEBIAN_FRONTEND=noninteractive apt-get update && \
    apt-get install -u -y --no-install-recommends \
        build-essential \
        ca-certificates \
        curl \
        git \
        pkg-config \
        python && \
    rm -rf /var/lib/apt/lists/*
 
# verify gpg and sha256: http://nodejs.org/dist/v0.10.30/SHASUMS256.txt.asc
# gpg: aka "Timothy J Fontaine (Work) <tj.fontaine@joyent.com>"
# RUN gpg --keyserver pgp.mit.edu --recv-keys 7937DFD2AB06298B2293C3187D33FF9D0246406D
COPY keysign.gpg /root/keysign_tjfontaine_expired.gpg

ENV NODE_VERSION 0.8.28
ENV NPM_VERSION 2.5.0
RUN curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz" \
&& curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/SHASUMS256.txt.asc" \
&& gpg --primary-keyring /root/keysign_tjfontaine_expired.gpg --verify SHASUMS256.txt.asc \
&& grep " node-v$NODE_VERSION-linux-x64.tar.gz\$" SHASUMS256.txt.asc | sha256sum -c - \
&& tar -xzf "node-v$NODE_VERSION-linux-x64.tar.gz" -C /usr/local --strip-components=1 \
&& rm "node-v$NODE_VERSION-linux-x64.tar.gz" SHASUMS256.txt.asc \
&& npm config set strict-ssl false \
&& npm install -g npm@1.4.28 \
&& npm install -g npm@"$NPM_VERSION" \
&& npm cache clear
# note: we have to install npm 1.4.28 first because we can't go straight from 1.2 -> 2.0
# see also https://github.com/docker-library/node/issues/15#issuecomment-57879931
CMD [ "node" ]
