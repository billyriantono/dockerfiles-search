FROM tim03/build-deps
LABEL maintainer Chen, Wenli <chenwenli@chenwenli.com>

RUN \
 cd /tmp && \
 wget https://storage.googleapis.com/golang/go1.7.5.linux-amd64.tar.gz && \
 tar xvzf go1.7.5.linux-amd64.tar.gz -C /usr/local

RUN \
 mkdir ~/go

ENV GOROOT /usr/local/go
ENV GOPATH /root/go
ENV PATH $PATH:$GOROOT/bin:$GOPATH/bin

CMD go version

