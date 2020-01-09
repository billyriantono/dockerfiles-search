#FROM alpine:latest
FROM mitchty/alpine-ghc
RUN mkdir hakylldemo
WORKDIR  hakylldemo
ADD hakylldemo.cabal .
# RUN stack setup
# RUN cabal init
RUN cabal configure

# RUN apk update
# RUN apk add --update gcc

# ???
RUN apk add --update cmake

RUN apk add --update libc-dev
RUN apk add --update zlib-dev
RUN apk add --update linux-headers
# RUN apk upgrade  gcc
# RUN gcc -v
# RUN stack install pandoc --system-ghc
RUN stack install hakyll --system-ghc
# RUN apk add --update curl
# RUN curl -sSL https://get.haskellstack.org/ | sh
# # RUN stack install haskell-tools-daemon-0.6.0.0 --resolver nightly-2017-04-05
# # RUN stack install haskell-tools-daemon-0.6.0.0 --resolver nightly-2017-04-05 --install-ghc
# RUN stack install hakyll --resolver nightly-2017-04-05 --install-ghc
# RUN stack install hakyll
