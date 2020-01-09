## ==============================
FROM tensorflow/tensorflow:1.14.0-gpu-py3  


ARG DEBIAN_FRONTEND=noninteractive


# todo: minimize this even more
RUN apt-get update -qq &&\
    apt-get install -qq --no-install-recommends \
        libopenblas-dev liblapack-dev libx11-dev \
        libavcodec-dev libavformat-dev libswscale-dev \
        libtbb2 libtbb-dev libjpeg-dev libboost-all-dev python3 \
        python-pip git g++-8 build-essential wget curl \
        make libprotobuf-dev protobuf-compiler libopencv-dev \
        libpng-dev libtiff-dev cmake apt-utils nano &&\
    rm -rf /var/lib/apt/lists/*
## ====================================================

##======================================================
# Install keras and update others package

RUN pip install setuptools 
RUN pip install face_alignment
RUN pip install scipy==1.3.1 
RUN pip install scikit-image==0.15.0 
RUN pip install keras==2.2.0
RUN pip install keras-vggface --no-dependencies 
RUN pip install -U keras_applications==1.0.6 --no-deps 
Run pip install -U scikit-learn 
##======================================================
##======================================================
##======================= Cmake =========================================
ARG DEBIAN_FRONTEND=noninteractive
#replace cmake as old version has CUDA variable bugs
RUN wget https://github.com/Kitware/CMake/releases/download/v3.14.2/cmake-3.14.2-Linux-x86_64.tar.gz && \
    tar xzf cmake-3.14.2-Linux-x86_64.tar.gz -C /opt && \
    rm cmake-3.14.2-Linux-x86_64.tar.gz 

ENV PATH /opt/cmake-3.14.2-Linux-x86_64/bin:$PATH

## ==================== Build-time dependency libs ======================
## This will build and install opencv and dlib into an additional dummy
## directory, /root/diff, so we can later copy in these artifacts,
## minimizing docker layer size
## Protip: ninja is faster than `make -j` and less likely to lock up system


WORKDIR /root/build-dep
ARG DEBIAN_FRONTEND=noninteractive

## ==================== Building dlib ===========================

RUN curl http://dlib.net/files/dlib-19.13.tar.bz2 -LO &&\
    tar xf dlib-19.13.tar.bz2 && \
    rm dlib-19.13.tar.bz2 &&\
    mv dlib-19.13 dlib &&\
    mkdir -p dlib/build &&\
    cd dlib/build &&\
    cmake .. -DCMAKE_CXX_FLAGS="-fPIC" && \
    cmake --build . --config Release -j 4 &&\
    make install && \
    ldconfig 

## ==================== Building OpenCV ======================
WORKDIR /root/build-dep
RUN curl https://github.com/opencv/opencv/archive/4.1.0.zip -LO &&\
    unzip 4.1.0.zip && \
    rm 4.1.0.zip &&\
    mv opencv-4.1.0 opencv

WORKDIR /root/build-dep/opencv/build

#RUN echo $PATH
RUN cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D BUILD_TIFF=ON -D WITH_TBB=ON -D BUILD_SHARED_LIBS=OFF .. &&\
    cmake --build . -j 4 && \
    make install
# RUN wget https://github.com/opencv/opencv/archive/4.1.0.zip &&\
#     unzip 4.1.0.zip && \
#     rm 4.1.0.zip &&\
#     mv opencv-4.1.0 opencv && \
#     mkdir -p opencv/build && \
#     cd opencv/build && \
#     cmake -D CMAKE_BUILD_TYPE=RELEASE \
#         -D CMAKE_INSTALL_PREFIX=/usr/local \
#         -D WITH_TBB=ON -D WITH_CUDA=OFF \
#         -DWITH_QT=OFF -DWITH_GTK=OFF\
# 	-D BUILD_SHARED_LIBS=OFF -D BUILD_TIFF=ON -D BUILD_EXAMPLES=OFF .. &&\
#     cmake --build . -j 4 &&\
#     make install
# ##========================  open face  ================================

WORKDIR /root/openface

RUN curl https://github.com/TadasBaltrusaitis/OpenFace/archive/OpenFace_2.2.0.zip -LO &&\
    unzip OpenFace_2.2.0.zip &&\
    rm OpenFace_2.2.0.zip

COPY OpenFaceWrapper /root/openface/OpenFaceWrapper

# RUN echo $PWD && \
#     ls && \
#     echo $LD_LIBRARY_PATH 
    
# RUN cd OpenFaceWrapper &&\
#     echo $PWD && \
#     ls && \
WORKDIR /root/openface/OpenFaceWrapper/build

RUN export LD_LIBRARY_PATH=/usr/lib/x86_64-linux-gnu/openblas:$LD_LIBRARY_PATH && \
    echo $LD_LIBRARY_PATH && \
    echo $PWD && \
    cmake -D OPENFACE_DIR='/root/openface/OpenFace-OpenFace_2.2.0' -D CMAKE_CXX_COMPILER=g++-8 -D CMAKE_C_COMPILER=gcc-8 -D    CMAKE_BUILD_TYPE=RELEASE ..   && \
    cmake --build . --target OpenFaceWrapper -j 4 
    # RUN cd openface_wrapper &&\
#     mkdir -p build && cd build && \
#     cmake -D OPENFACE_DIR='/root/openface/OpenFace_2.2.0'-D CMAKE_CXX_COMPILER=g++-8 -D CMAKE_C_COMPILER=gcc-8 -D    CMAKE_BUILD_TYPE=RELEASE .. &&\
#     cmake --build . --target openface_wrapper -j 4 
# ##=======================================================
# # Since we "imported" the build artifacts, we need to reconfigure ld


# Since we "imported" the build artifacts, we need to reconfigure ld
RUN ldconfig
