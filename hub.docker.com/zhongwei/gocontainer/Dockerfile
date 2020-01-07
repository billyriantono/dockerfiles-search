FROM zhongwei/container

MAINTAINER Wei Zhong <zhongwei99@163.com>

# Install Go
RUN wget https://storage.googleapis.com/golang/go1.7.5.linux-amd64.tar.gz && \
    tar -C /usr/local -xzf go1.7.5.linux-amd64.tar.gz && \
    rm go1.7.5.linux-amd64.tar.gz

ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"
WORKDIR $GOPATH