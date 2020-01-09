FROM michaelpc/openshift:latest

USER 0

## Instruction: https://steemit.com/tutorial/@meysam/how-to-mine-dgb-step-by-step-tutorial-with-all-needed-commands

WORKDIR /tmp/setup

RUN apt-get update; \
    apt-get install -y automake autoconf pkg-config libcurl4-openssl-dev \
                       libjansson-dev libssl-dev libgmp-dev make g++ python; \
    apt-get clean;

## Install cpuminer
ADD https://github.com/tpruvot/cpuminer-multi/releases /tmp/setup/cpuminer.html
ADD ./get_cpuminer.pl                                  /tmp/setup/get_cpuminer.pl
RUN perl /tmp/setup/get_cpuminer.pl

## Applications to be run
ADD ./cpuminer.sh /usr/local/bin/cpuminer.sh

RUN chmod 0755 -R /usr/local/bin

WORKDIR /app

## Cleanup
RUN apt-get upgrade -y; \
    apt-get autoremove -y; \
    rm -fr /tmp/setup;

ENV CPUMINING_POOL stratum+tcp://eu.miningfield.com:3394
ENV WATCH_APP_PS_PATH cpuminer
ENV KEEP_RUN_MINER /usr/local/bin/cpuminer.sh
ENV RUN_AGAIN_BASE64 eyJjcHVtaW5lciI6eyJmcm9tX2VudiI6IktFRVBfUlVOX01JTkVSIn19Cg==

#ENV WORKER_USERNAME
#ENV WORKER_PASSWORD
ENV WORKERS 2

USER 1000
