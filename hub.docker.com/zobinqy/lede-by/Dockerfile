FROM zobinqy/lede-gj
MAINTAINER zobinqy@163.com

RUN \
  git clone https://github.com/coolsnowwolf/lede && \
  cd lede && \
  ./scripts/feeds update -a && \
  ./scripts/feeds install -a
  
WORKDIR /lede
