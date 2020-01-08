FROM haskell:8.4.4

WORKDIR /usr/src/app

RUN apt-get update && apt-get install -y libleveldb-dev leveldb-doc openssh-client expat libexpat1-dev libpq-dev xz-utils make
RUN stack upgrade

COPY ./snapshot.yaml .
COPY ./stack.yaml .
COPY ./package.yaml .

RUN stack install --no-docker --only-dependencies --system-ghc

# Only copy necessary files
COPY src ./src
COPY config ./config
COPY bench ./bench
COPY exe ./exe
COPY postgres ./postgres
COPY tests ./tests
COPY README.md .
COPY network-profile ./network-profile
COPY sdk ./sdk

RUN stack install --no-docker --system-ghc
