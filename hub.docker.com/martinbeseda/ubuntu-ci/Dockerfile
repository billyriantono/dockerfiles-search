FROM ubuntu:latest

RUN apt-get clean && apt-get update && apt-get install -y -V make build-essential g++-8 wget git gcc gfortran pkg-config mpich python python3 bison flex

# Download the new version of CMake and "install" it
RUN wget https://github.com/Kitware/CMake/releases/download/v3.16.0-rc3/cmake-3.16.0-rc3-Linux-x86_64.sh
RUN chmod +x cmake-*.sh
RUN yes | ./cmake-3.16.0-rc3-Linux-x86_64.sh
WORKDIR "cmake-3.16.0-rc3-Linux-x86_64/bin"
RUN ln -s $(pwd)/cmake /usr/bin/cmake
