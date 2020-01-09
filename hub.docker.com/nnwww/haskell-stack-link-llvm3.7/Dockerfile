FROM nnwww/haskell-stack-link
LABEL description="Build static binary with llvm3.7 (for ghc8)"
MAINTAINER Nnwww <johndororo@gmail.com>

# install llvm3.7
RUN apk update && apk upgrade && \
    apk add llvm3.7
