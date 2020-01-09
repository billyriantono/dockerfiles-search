# Start from cuda/cudnn docker image
FROM alexwitt23/tracker_base:base

RUN apt-get update \
    && apt-get install -y \
        tar \
        spin \
        libavcodec57 \
        libavformat57 \
        libswscale4 \ 
        libswresample2 \ 
        libavutil55 \
        libusb-1.0-0 \
        libgtkmm-2.4-dev \
    && rm -rf /var/lib/apt/lists/*
    
RUN cd /data/sources && git clone https://github.com/alexwitt2399/tracker.git

WORKDIR /data/sources/tracker

RUN mv spinnaker-1.26.0.31-amd64 /data/sources/spinnaker \
    && cd ../spinnaker \
    && sh install_spinnaker.sh

RUN export LD_LIBRARY_PATH=/usr/local/cuda/lib64/stubs:$LD_LIBRARY_PATH && \
    ln -s /usr/local/cuda/lib64/stubs/libcuda.so /usr/lib/x86_64-linux-gnu/libcuda.so.1
    
RUN make CONF=Debug_Blackfly \
    && ln -s yolotracker.json /data/sources/tracker/dist/Debug_Blackfly/GNU-Linux/yolotracker.json 

RUN make CONF=Debug_Blackfly_cv4 \
    && ln -s yolotracker.json /data/sources/tracker/dist/Debug_Blackfly_cv4/GNU-Linux/yolotracker.json 

RUN make CONF=Debug \
    && ln -s yolotracker.json /data/sources/tracker/dist/Debug/GNU-Linux/yolotracker.json 

RUN make CONF=Debug_cv4 \
    && ln -s yolotracker.json /data/sources/tracker/dist/Debug_cv4/GNU-Linux/yolotracker.json 

RUN mv /data/sources/tracker /data/sources/yolotracker
