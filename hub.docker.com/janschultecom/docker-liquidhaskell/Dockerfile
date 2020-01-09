FROM haskell:8.2.2


RUN apt-get upgrade \
    && apt-get update \
    && apt-get install -y z3 \
    && git clone --recursive https://github.com/ucsd-progsys/liquidhaskell.git \
    && cd liquidhaskell \
    && stack install

# TODO: Should use liquid user
#RUN useradd -r -m liquid
#USER liquid

VOLUME /data

WORKDIR /data

ENTRYPOINT /bin/bash
