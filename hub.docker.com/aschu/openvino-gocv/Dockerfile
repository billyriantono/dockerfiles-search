FROM aschu/openvino:latest
LABEL maintainer="Alex Schultz. mail: alex.c.schultz@gmail.com"

RUN apt-get update
RUN apt-get install -y software-properties-common

# Install FFmpeg
RUN add-apt-repository ppa:jonathonf/ffmpeg-3

RUN apt-get install -y ffmpeg libav-tools x264 x265
RUN apt-get install -y wget
RUN apt-get install -y git

# Install Go
RUN wget https://dl.google.com/go/go1.11.linux-amd64.tar.gz && \
 tar -C /usr/local -xzf go1.11.linux-amd64.tar.gz && \
 rm go1.11.linux-amd64.tar.gz

# Setup GoPath
RUN mkdir $HOME/go
ENV GOPATH=$HOME/go
ENV PATH=$PATH:/usr/local/go/bin

# Install gocv
RUN go get -u -d gocv.io/x/gocv
RUN cd $GOPATH/src/gocv.io/x/gocv && \
 make install && \
 make clean

# Container Setup
WORKDIR $GOPATH

CMD ["bash"]
