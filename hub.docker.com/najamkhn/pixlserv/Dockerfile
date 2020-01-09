FROM golang
MAINTAINER Najam Khan <n@najamkhn.com>

ENV PROJECT_DIR /go/src/pixlserv/
ENV PROJECT_REPO https://github.com/rhime/pixlserv.git

RUN git clone --depth=2 $PROJECT_REPO $PROJECT_DIR
RUN cd $PROJECT_DIR && go get && go build && ls -al && \
    ln -s /go/src/pixelserv/pixelserv /usr/local/bin

EXPOSE 3000

