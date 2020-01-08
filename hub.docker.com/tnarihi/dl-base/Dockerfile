FROM tnarihi/python:cuda7.5-cudnn4
RUN apt-get install -y wget
RUN wget https://cmake.org/files/v3.1/cmake-3.1.3.tar.gz
RUN tar xvf cmake-3.1.3.tar.gz
RUN apt-get install -y cmake
ENV CMAKE_PATH /opt/cmake-3.1.3
RUN cd cmake-3.1.3 && mkdir build && cd build && cmake -D CMAKE_INSTALL_PREFIX=${CMAKE_PATH} .. && make && make install
ENV PATH $CMAKE_PATH/bin:${PATH}
RUN cd ../.. && rm -rf cmake-3.1.3
RUN apt-get install -y unzip
RUN pip install cython
RUN pip install pytest
RUN pip install pytest-rerunfailures
RUN apt-get install -y clang-format-3.4
RUN apt-get install -y zsh
RUN pip install theano
