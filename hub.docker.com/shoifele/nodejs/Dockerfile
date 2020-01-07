# shoifele/nodejs

FROM shoifele/bone

MAINTAINER Christoph Wiechert <wio@psitrax.de>

ENV REFRESHED_AT="2015-25-12"
ENV NODE_VERSION="4.2.1"

## install anything we need in one turn
RUN mkdir -p /opt/nodejs && cd /opt/nodejs && \
    curl -s -L https://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-x64.tar.gz \
      | tar xz --strip 1 && \
    ln -s /opt/nodejs/bin/node /usr/local/bin/node && \
    ln -s /opt/nodejs/bin/npm /usr/local/bin/npm 

ADD rootfs /

CMD ["/init"]
