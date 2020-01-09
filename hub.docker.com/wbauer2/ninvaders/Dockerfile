FROM debian:stretch-slim
LABEL maintainer="wbauer2 <wbauer2@wisc.edu>"

# Debian Base to use
ENV DEBIAN_VERSION stretch

# Install the games we want 
RUN echo "deb http://ftp.us.debian.org/debian $DEBIAN_VERSION main contrib nonfree" > /etc/apt/sources.list && \
    echo "deb http://ftp.us.debian.org/debian $DEBIAN_VERSION-updates main contrib non-free" >> /etc/apt/sources.list && \
    echo "deb http://security.debian.org/ $DEBIAN_VERSION/updates main contrib non-free" >> /etc/apt/sources.list && \
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y -qq \
	ninvaders && \
    apt-get clean

ADD play_nInvaders.sh /
CMD ["/play_nInvaders.sh"]
