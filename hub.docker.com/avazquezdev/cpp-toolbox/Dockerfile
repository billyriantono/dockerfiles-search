FROM debian:latest

# Install packages and tools needed to compile source code.
RUN apt-get update && \
    apt-get install -y \
        clang \
        cmake \
        cppcheck \
        gdbserver \
        graphviz \
        libgtest-dev \
        ninja-build \
        valgrind \
     # Save space.
     && apt-get autoclean \
     && apt-get autoremove \
     # Compile googletest.
     && cd /usr/src/gtest \
     && cmake CMakeLists.txt \
     && make \
     && cp *.a /usr/lib/

WORKDIR /home/project

# Expose the remote debugging session on port 8000.
EXPOSE 8000

ENTRYPOINT [ "/bin/bash" ]