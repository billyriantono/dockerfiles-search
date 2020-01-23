from genoteam/gcc-cmake-eigen:latest

# install doctest for unit testing
workdir /tmp
run git clone https://github.com/onqtam/doctest.git --depth=1 --branch master --single-branch
workdir doctest/build
run \
  cmake -D CMAKE_BUILD_TYPE=Release .. && \
  cmake --build . && \
  cmake --build . --target install
workdir /
run rm -rf /tmp/doctest

