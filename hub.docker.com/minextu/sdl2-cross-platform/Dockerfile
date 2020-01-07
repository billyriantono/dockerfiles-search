FROM minextu/mingw-sdl2-debian:latest
MAINTAINER minextu

# install sdl
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        libsdl2-dev                            \
        libsdl2-ttf-dev                        \
        libsdl2-image-dev                   && \
    rm -rf /var/lib/apt/lists/*

# install build tools
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        ca-certificates                        \
        zip                                    \
        python                                 \
        openssh-client                      && \
    rm -rf /var/lib/apt/lists/*

# install emscripten
RUN cd /opt && \
    wget https://s3.amazonaws.com/mozilla-games/emscripten/releases/emsdk-portable.tar.gz && \
    tar -xf emsdk-portable.tar.gz                  && \
    rm emsdk-portable.tar.gz                       && \
    cd emsdk-portable                              && \
    ./emsdk install -j2 --build=MinSizeRel latest  && \
    ./emsdk activate latest                        && \
    echo "source $(pwd)/emsdk_env.sh" >> ~/.bashrc

CMD /bin/bash
