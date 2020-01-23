# tmate-slave, see https://tmate.io/
#
# Example usage:
#
#     docker run --rm -i -p 22000:22000 -v /etc/tmate:/etc/tmate varac/tmate-slave

FROM library/ubuntu:18.04


ENV LANG en_US.utf8

RUN apt-get update && \
    apt-get install -y \
                    automake \
                    build-essential \
                    cmake \
                    git \
                    libevent-dev \
                    libmsgpack-dev \
                    libncurses-dev \
                    libssh-dev \
                    libssl-dev \
                    libtool \
                    locales \
                    pkg-config \
                    ruby \
                    zlib1g-dev \
                    zlib1g-dev

RUN localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8


COPY . /src/tmate-slave
WORKDIR /src/tmate-slave
RUN sh autogen.sh && \
      PKG_CONFIG_PATH=/usr/local/lib/pkgconfig ./configure && \
      make && \
      cp /src/tmate-slave/tmate-slave /sbin/

# Final container build stage

FROM library/ubuntu:18.04

ENV LANG en_US.utf8

RUN apt-get update && \
    apt-get install -y \
                    dumb-init \
                    libevent-dev \
                    libmsgpack-dev \
                    libssh-4 \
                    locales \
                    openssh-client && \
    rm -rf /var/lib/apt/*

RUN localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8

COPY --from=0 /src/tmate-slave/tmate-slave /sbin/
COPY --from=0 /src/tmate-slave/docker-entrypoint.sh /bin
COPY --from=0 /src/tmate-slave/create_keys.sh /bin

VOLUME /etc/tmate
EXPOSE 22000

ENTRYPOINT [ "/usr/bin/dumb-init" ]
CMD [ "/bin/docker-entrypoint.sh", "-k", "/etc/tmate/keys", "-b", "0.0.0.0", "-p", "22000", "-v" ]
