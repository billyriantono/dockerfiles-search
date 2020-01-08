FROM debian:latest
RUN apt-get update && apt-get install vim git ghc make cabal-install -y && cabal update && cabal install cmark-gfm missingH split
RUN apt-get install unzip zlib1g-dev -y && cabal install pandoc
ENTRYPOINT [""]
CMD bash
