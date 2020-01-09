FROM prsam/hpx_base:latest

RUN export N_CORES=$(grep -c ^processor /proc/cpuinfo)                      && \
    git clone --depth=1 https://github.com/STEllAR-GROUP/hpx.git /hpx       && \
    mkdir -p /hpx/build                                                     && \
    cd /hpx/build && cmake -DCMAKE_BUILD_TYPE=Release                          \
                           -DHPX_WITH_MALLOC=system                            \
                           -DHPX_WITH_GIT_COMMIT=$(git rev-parse HEAD)         \
                           -DCMAKE_CXX_FLAGS='-fcolor-diagnostics'             \
                           -DHPX_WITH_TESTS_HEADERS=Off                        \
                           -DHPX_WITH_DEPRECATION_WARNINGS=Off                 \
                           -DCMAKE_EXPORT_COMPILE_COMMANDS=On ..            && \
    cmake --build /hpx/build -- -j$N_CORES examples.quickstart.hello_world  && \
    cmake --build /hpx/build -- -j$N_CORES install                          && \
    rm -rf /hpx/build                                                       && \
    ldconfig
