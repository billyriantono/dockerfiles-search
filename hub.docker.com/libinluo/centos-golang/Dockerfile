FROM libinluo/centos:1.0.0

RUN yum -y install unzip \
    && yum -y clean all

RUN cd tmp \
    && curl -OL https://storage.googleapis.com/golang/go1.5.4.linux-amd64.tar.gz \
    && tar -C /usr/local -xzf go1.5.4.linux-amd64.tar.gz \
    && rm -rf go1.5.4.linux-amd64.tar.gz \
    && echo "export PATH=$PATH:/usr/local/go/bin" >> /etc/profile

ENV PATH=$PATH:/usr/local/go/bin

ENV GOPATH /go
RUN mkdir -p $GOPATH/{bin,main,pkg,src} && chmod -R 777 $GOPATH
ENV PATH $GOPATH/bin:$PATH
WORKDIR $GOPATH
