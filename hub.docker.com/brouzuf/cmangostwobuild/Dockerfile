FROM linuxserver/mariadb

RUN \
  apt-get --assume-yes update && apt-get --assume-yes upgrade && \
  apt-get --assume-yes install build-essential gcc g++ automake git-core autoconf make patch \
  libmysql++-dev libtool libssl-dev grep binutils zlibc libc6 libbz2-dev cmake subversion \
  libboost-all-dev mysql-client-5.6 screen libace-dev 

RUN \
  git clone https://github.com/cmangos/mangos-wotlk.git /sources --recursive -b master && \
  git clone https://github.com/cmangos/wotlk-db.git /database --recursive -b master && \
  git clone https://github.com/brouzuf/CmangosWotLK.git /install --recursive -b master

RUN \
  mkdir "/sources/build" && cd "/sources/build" && \
  cmake .. -DCMAKE_INSTALL_PREFIX="/mangos" -DDEBUG=0 -DPCH=1 -DBUILD_EXTRACTORS=ON -DBUILD_PLAYERBOT=ON && \
make

RUN \
  mkdir /mangos && \
cp -a /sources/build/contrib/extractor/ad /mangos && \
cp -a /sources/build/contrib/mmap/MoveMapGen /mangos && \
cp -a /sources/build/contrib/vmap_assembler/vmap_assembler /mangos && \
cp -a /sources/build/contrib/vmap_extractor/vmapextract/vmap_extractor /mangos && \
cp -a /sources/contrib/extractor_scripts/*.* /mangos && \
cp -a /sources/build/src/mangosd/mangosd /mangos && \
cp -a /sources/build/src/realmd/realmd /mangos && \
cp -a -R /sources/sql/create /database/create && \
cp -a -R /sources/sql/base /database/base && \
cp -a -R /sources/sql/tools /database/tools && \
cp -a -R /sources/doc /mangos/Docs
