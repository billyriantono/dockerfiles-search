FROM sglim2/centos7
MAINTAINER <caidongqiang@hotmail.com>

# install libfastcommon
RUN cd /tmp && git clone https://github.com/happyfish100/libfastcommon.git && \
    cd libfastcommon && \
    ./make.sh && \ 
    ./make.sh install 

RUN ln -s /usr/lib64/libfastcommon.so /usr/local/lib/libfastcommon.so && \
    ln -s /usr/lib64/libfdfsclient.so /usr/local/lib/libfdfsclient.so && \
    ln -s /usr/lib64/libfdfsclient.so /usr/lib/libfdfsclient.so

# install fastDFS
RUN cd /tmp && \
    git clone https://github.com/happyfish100/fastdfs.git && \
    cd fastdfs && \
    ./make.sh && \
    ./make.sh install && \
    rm -rf /tmp/*

