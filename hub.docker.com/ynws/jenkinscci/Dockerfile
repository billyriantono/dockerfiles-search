FROM jenkins

USER root

RUN apt-get update && \
    apt-get install -y \
                    g++ \
                    cmake \
                    gcovr \
                    cppcheck \
                    doxygen \
                    graphviz \
                    && \
    rm -rf /var/lib/apt/lists/*

RUN cd /usr/src && \
    wget https://github.com/google/googletest/archive/release-1.8.0.tar.gz && \
    tar xvzf release-1.8.0.tar.gz && \
    rm release-1.8.0.tar.gz

RUN cd /usr/src/googletest-release-1.8.0 && \
    mkdir build && \
    cd build && \
    cmake .. && \
    make

USER jenkins

