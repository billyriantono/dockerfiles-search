FROM golang:1.12.7-alpine3.10

ENV REQPACKAGES='python3 openblas libstdc++'
ENV DEVPACKAGES='gcc gfortran python3-dev build-base openblas-dev git subversion'

RUN apk add --no-cache ${REQPACKAGES} ${DEVPACKAGES} 
# install zeromq
RUN mkdir /src && cd /src && git clone https://github.com/zeromq/libzmq && cd libzmq \
    && apk add libtool autoconf automake \
    && ./autogen.sh && ./configure && make -j 4 \
    && make install && ldconfig; \
    rm -fr /src/libzmq

RUN pip3 install cython numpy jsonpickle scipy scikit-learn pyzmq pygam pandas xlrd 
