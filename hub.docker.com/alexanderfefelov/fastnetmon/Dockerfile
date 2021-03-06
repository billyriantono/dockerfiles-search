FROM ubuntu:18.04 AS build

ARG COMMIT_HASH=998b21d

WORKDIR /tmp

RUN  apt-get -qq update \
  && apt-get -qq --no-install-recommends install ca-certificates git wget net-tools \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/* \
  && git clone https://github.com/pavel-odintsov/fastnetmon.git \
  && cd fastnetmon \
  && git checkout ${COMMIT_HASH} \
  && echo none@inter.net | perl src/fastnetmon_install.pl --use-modern-pf-ring --do-not-track-me

FROM ubuntu:18.04

ENV DEBIAN_FRONTEND noninteractive

RUN  apt-get -qq update \
  && apt-get -qq --no-install-recommends install  ca-certificates openssh-client sshpass \
       libboost-thread1.65.1 \
       libboost-program-options1.65.1 \
       libboost-regex1.65.1 \
       libnuma1 \
       libpcap0.8 \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

COPY --from=build /opt /opt

COPY container/ /

VOLUME /fastnetmon
VOLUME /var/log/fastnetmon_attacks

CMD ["/fastnetmon/bin/fastnetmon.sh"]
