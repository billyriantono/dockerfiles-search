FROM icsinc/qt5.5.0-x64

# install lapack/blas/f2c
RUN add-apt-repository main
RUN add-apt-repository universe
RUN add-apt-repository restricted
RUN add-apt-repository multiverse
RUN apt-get update
RUN apt-get install -y liblapack-dev f2c

# add  cmake-3.x and zeromq to repository
RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:george-edison55/cmake-3.x
RUN add-apt-repository ppa:chris-lea/zeromq
RUN apt-get update
RUN apt-get upgrade -y

# install cmake and zeromq
RUN apt-get install -y cmake
RUN apt-get install -y libzmq3-dev libzmq3


