FROM ubuntu:18.04

RUN apt-get update \
  && apt-get install -y curl \
  && rm -rf /var/lib/apt/lists/* /var/cache/apt/*

ENV ZOLA_VERSION=v0.8.0

RUN curl -L https://github.com/getzola/zola/releases/download/$ZOLA_VERSION/zola-$ZOLA_VERSION-x86_64-unknown-linux-gnu.tar.gz > zola.tar.gz \
  && tar xvf zola.tar.gz \
  && mv zola /usr/bin/ \
  && rm -rf zola.tar.gz

WORKDIR /zola

EXPOSE 1111

CMD ["zola", "serve", "-i", "0.0.0.0"]
