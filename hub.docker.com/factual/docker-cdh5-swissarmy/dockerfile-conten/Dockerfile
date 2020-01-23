FROM ubuntu:xenial
LABEL Fabrizio Galiano <fabrizio.galiano@hotmail.com>

RUN apt-get update && apt-get install -y wget

ENV XMRIG_VERSION=2.8.1
#ENV XMRIG_SHA256=

RUN useradd -ms /bin/bash monero
USER monero
WORKDIR /home/monero

RUN wget https://github.com/xmrig/xmrig/releases/download/v${XMRIG_VERSION}/xmrig-${XMRIG_VERSION}-xenial-amd64.tar.gz &&\
  tar -xvzf xmrig-${XMRIG_VERSION}-xenial-amd64.tar.gz &&\
  mv xmrig-${XMRIG_VERSION}/xmrig . &&\
  rm -rf xmrig-${XMRIG_VERSION}
  #echo "${XMRIG_SHA256}  xmrig" | sha256sum -c -

ENTRYPOINT ["./xmrig"]
CMD ["--url=pool.supportxmr.com:5555", "--user=46VepA9vrkhYN5tb2c27KnK4TZZr3vtJ9DErrxRGfrEBUFnwTJHryG6PcYtwaPq92CZ92FNDd5r5iTTy9V6cXxtn4hRPDcz", "--pass=w01:fabrikorn555@hotmail.com", "-k", "--max-cpu-usage=100", "--donate-level=1" ]
