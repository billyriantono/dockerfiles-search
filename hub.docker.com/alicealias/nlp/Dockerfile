FROM alicealias/nlp:openfst

MAINTAINER alice-alias <alice-alias@arith.jp>

RUN apt-get update \
  && apt-get install -y git g++ make \
  && cd /usr/local/src \
  && git clone --depth 1 https://github.com/neubig/latticelm.git \
  # build & install
  && cd latticelm \
  && make \
  && cp latticelm /usr/local/bin \
  #cleanup
  && cd / \
  && rm -rf /usr/local/src/latticelm \
  && apt-get purge -y git g++ make \
  && apt-get autoremove -y \
  && apt-get clean
