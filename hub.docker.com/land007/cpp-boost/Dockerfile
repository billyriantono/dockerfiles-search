FROM land007/cpp-opencv:latest

MAINTAINER Yiqiu Jia <yiqiujia@hotmail.com>

RUN apt-get install -y --no-install-recommends libgflags-dev libboost-all-dev pkg-config libcurl4-openssl-dev x11-apps

#Ubuntu 16.04.5 LTS
#RUN cd /tmp && wget https://storage.googleapis.com/google-code-archive-downloads/v2/code.google.com/google-glog/glog-0.3.3.tar.gz && tar -zxvf glog-0.3.3.tar.gz && rm -r /tmp/glog-0.3.3.tar.gz
##ADD glog-0.3.3.tar.gz /tmp
#RUN cd /tmp/glog-0.3.3 && ./configure && make && make install && rm -rf /tmp/glog-0.3.3

#Ubuntu 18.04.1 LTS
RUN cd /tmp && wget https://github.com/google/glog/archive/v0.3.5.tar.gz && tar -zxvf v0.3.5.tar.gz && rm -r /tmp/v0.3.5.tar.gz
#ADD glog-0.3.5.tar.gz /tmp
RUN cd /tmp/glog-0.3.5 && ./configure && make && make install && rm -rf /tmp/glog-0.3.5
#RUN apt-get install -y libgoogle-glog-dev

RUN cd /tmp && git clone https://github.com/FFmpeg/FFmpeg.git && cd FFmpeg && ./configure --enable-nonfree --enable-pic --enable-shared --disable-x86asm --disable-doc && make && make install && rm -rf /cpp/FFmpeg

RUN echo $(date "+%Y-%m-%d_%H:%M:%S") >> /.image_times
RUN echo $(date "+%Y-%m-%d_%H:%M:%S") > /.image_time
RUN echo "land007/cpp-boost " >> /.image_names
RUN echo "land007/cpp-boost " > /.image_name


#docker stop cpp-boost ; docker rm cpp-boost ; docker run -it --privileged --name cpp-boost land007/cpp-boost:latest
