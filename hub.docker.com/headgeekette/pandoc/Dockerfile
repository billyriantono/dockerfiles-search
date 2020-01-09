FROM haskell:8.4
MAINTAINER Charo Nuguid <me@thegeekettespeaketh.com>

RUN apt-get update \
        && apt-get install -y wget \
        && apt-get clean

# Download pandoc
RUN mkdir pandoc \
        && cd pandoc \
        && wget https://hackage.haskell.org/package/pandoc-2.3.1/pandoc-2.3.1.tar.gz \
        && tar xvzf pandoc-2.3.1.tar.gz \
        && cd pandoc-2.3.1

# update cabal, install pandoc, clean up
RUN cabal update \
        && cabal install pandoc \
        && cd \
        && rm -rf /pandoc
ENV PATH $PATH:/root/.cabal/bin

ENTRYPOINT ["/root/.cabal/bin/pandoc"]

CMD ["--help"]
