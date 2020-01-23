###############################################################################
# quarter@ubuntu
###############################################################################
# /
# |-- build
# |   `-- quarter         <-- build directory
# |-- [rw] export	      <-- output package directory
# |-- [ro] import         <-- input source repository
###############################################################################
FROM ggabbiani/coin:ubuntu
MAINTAINER Giampiero Gabbiani "giampiero@gabbiani.org"

###############################################################################
# directory structure setup
RUN mkdir -p /build/quarter
WORKDIR /build/quarter

###############################################################################
# quarter system pre requisites install
RUN apt-get install -y qttools5-dev

###############################################################################
# pre requisites install from BitBucket repository
RUN wget https://bitbucket.org/ggabbiani/coin-fork/downloads/ubuntu-build.tgz \
 && tar -xzf ubuntu-build.tgz \
 && dpkg -i $(cat artifacts.list)

###############################################################################
# defaults for building from a mounted project source
CMD cmake /import \
      -DCMAKE_BUILD_TYPE=MinSizeRel \
      -DQUARTER_BUILD_DOC_QTHELP=ON \
  && make -j8 \
  && cpack --config cpack.d/debian.cmake \
  && dpkg -i $(cat cpack.d/artifacts.list) \
  && cp $(cat cpack.d/artifacts.list) /export/
