FROM        ubuntu:18.04

WORKDIR     /tmp/workdir

RUN     apt-get -yqq update && \
        apt-get install -yqq --no-install-recommends ca-certificates && \
        rm -rf /var/lib/apt/lists/*

RUN     apt-get -yqq update && \
        apt-get --no-install-recommends -yqq install python git && \
        rm -rf /var/lib/apt/lists/*

MAINTAINER  Colin McFadden <mcfa0086@umn.edu>

RUN         git clone https://github.com/google/spatial-media.git
WORKDIR     /tmp/workdir/spatial-media/

ENTRYPOINT  ["python", "spatialmedia"]

