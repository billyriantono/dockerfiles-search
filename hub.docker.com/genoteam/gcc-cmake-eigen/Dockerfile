from genoteam/gcc-cmake:latest

workdir /tmp
run git clone https://github.com/eigenteam/eigen-git-mirror.git --depth=1 --branch master --single-branch eigen
workdir eigen/build
run \
  cmake -D CMAKE_BUILD_TYPE=Release .. && \
  cmake --build . && \
  cmake --build . --target install
workdir /
run rm -rf /tmp/eigen
