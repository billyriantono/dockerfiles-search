FROM ubuntu:latest AS prep

ENV GOSU_VERSION 1.11
RUN set -x \
        && apt-get update && apt-get install -y --no-install-recommends \
                ca-certificates \
                gnupg \
                wget \
        && wget -O /tmp/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture)" \
        && wget -O /tmp/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture).asc" \
        && export GNUPGHOME="$(mktemp -d)" \
        && gpg --keyserver ipv4.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 \
        && gpg --batch --verify /tmp/gosu.asc /tmp/gosu

########

FROM ubuntu:latest

COPY --from=prep /tmp/gosu /usr/local/bin

ARG USER_ID
ARG GROUP_ID

# add user with specified (or default) user/group ids
ENV USER_ID ${USER_ID:-1000}
ENV GROUP_ID ${GROUP_ID:-1000}

# add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added
RUN groupadd -g ${GROUP_ID} hello \
        && useradd -u ${USER_ID} -g hello -s /bin/bash -m -d /hello hello

ENV HOME /hello
WORKDIR /hello

ADD https://beta.namecoin.org/files/namecoin-core/namecoin-core-0.18.0/namecoin-0.18.0-x86_64-linux-gnu.tar.gz /tmp
RUN tar -zxvf /tmp/namecoin-0.18.0-x86_64-linux-gnu.tar.gz -C /tmp \
        && su -c 'install -m 0755 -o root -g root -t /usr/local/bin /tmp/namecoin-0.18.0/bin/*' \
        && rm -rf /tmp/*

# grab gosu for easy step-down from root
RUN chmod +x /usr/local/bin/gosu \
        && gosu nobody true

# EXPOSE 8334 8335
COPY bin/*.sh /usr/local/bin/
CMD ["oneshot.sh"]
