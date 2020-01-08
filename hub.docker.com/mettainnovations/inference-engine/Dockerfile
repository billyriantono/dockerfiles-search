FROM mettainnovations/ubuntu-base:latest

RUN mkdir -p /home/developer
ENV HOME /home/developer
WORKDIR /home/developer

# Download and Install dldt
RUN git clone https://github.com/opencv/dldt.git && \
    cd dldt && \
    git checkout 2018_R4 && \
    git submodule init && \
    git submodule update --recursive && \
    cd inference-engine && \
    #./install_dependencies.sh && \
    mkdir build && \
    cd build && \
    cmake .. && \
    make -j4 

# Download and Install Model Zoo
RUN cd ~ && \
    git clone https://github.com/opencv/open_model_zoo.git && \
    cd open_model_zoo && \
    git checkout 2018_R4 && \
    git submodule init && \
    git submodule update

# Copy libs to /usr/local
RUN cd ~/dldt && \
    cp -R inference-engine /usr/local/lib/inference-engine 

# Move includes to /usr/local
RUN cd ~/dldt && \
    cp -R inference-engine /usr/local/include/inference-engine && \
    cd ~ && \
    cp -R open_model_zoo /usr/local/include/open_model_zoo

