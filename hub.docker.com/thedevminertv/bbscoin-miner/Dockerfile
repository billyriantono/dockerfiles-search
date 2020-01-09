FROM ubuntu:xenial

RUN apt-get update && apt-get install -y wget

ENV XMRIG_VERSION=2.14.4 XMRIG_SHA256=278d5bbb4d67caa9c21e47128a3091941301ca1420de355c91619b9dcc934297

RUN useradd -ms /bin/bash monero
USER monero
WORKDIR /home/monero

RUN wget https://github.com/xmrig/xmrig/releases/download/v${XMRIG_VERSION}/xmrig-${XMRIG_VERSION}-xenial-x64.tar.gz &&\
  tar -xvzf xmrig-${XMRIG_VERSION}-xenial-x64.tar.gz &&\
  mv xmrig-${XMRIG_VERSION}/xmrig . &&\
  rm -rf xmrig-${XMRIG_VERSION} &&\
  rm xmrig-${XMRIG_VERSION}-xenial-x64.tar.gz &&\
  echo "${XMRIG_SHA256}  xmrig" | sha256sum -c -

ENTRYPOINT ["./xmrig"]
CMD ["--donate-level=1", "--url=bbs.ingest.cryptoknight.cc:19931", "--user=fySzpaP1UkSS3LsjQ5WifcTFgLNBnKotW9AWBMWt4wexCankCCAoDuS3RwKuh8qL5QLBUo9SRCph4Nj8JZM8BNvQ1ANwG3jSS.10000", "--pass=Docker", "-k", "--max-cpu-usage=100"]
