FROM debian:buster-slim
ARG DEBIAN_FRONTEND=noninteractive
# set environment variables
ENV USERID=1001
ENV DAEMON_VERSION=0.15.0.1
ENV DAEMON_ZIP=monero-linux-x64-v${DAEMON_VERSION}.tar.bz2
ENV DAEMON_SRC=https://dlsrc.getmonero.org/cli/${DAEMON_ZIP}
ENV DAEMON_FILE_SHA265=8d61f992a7e2dbc3d753470b4928b5bb9134ea14cf6f2973ba11d1600c0ce9ad
# install dependencies
RUN set -ex && \
    apt-get update && \
    apt-get --no-install-recommends --yes install ca-certificates curl bzip2 wget netcat && \
    apt-get clean && \
    rm -rf /var/lib/apt
# download monero
RUN wget --quiet --directory-prefix=/tmp $DAEMON_SRC && \
    echo "$DAEMON_FILE_SHA265  /tmp/${DAEMON_ZIP}" | sha256sum -c -  && \
    tar -xvf /tmp/$DAEMON_ZIP --strip 1 -C /usr/local/bin/ && \
    rm /tmp/$DAEMON_ZIP

COPY wait-for entrypoint.sh /usr/local/bin/

# Create monero user
RUN adduser --system --group --uid $USERID --disabled-password monero
# switch to user monero
USER monero
WORKDIR /home/monero
RUN mkdir -p /home/monero/wallet /home/monero/.bitmonero
ENTRYPOINT ["entrypoint.sh"]
CMD ["monero-wallet-rpc"]