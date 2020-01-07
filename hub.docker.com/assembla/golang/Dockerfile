FROM assembla/ubuntu
MAINTAINER Artiom Di <kron82@gmail.com>

RUN apt-get install --no-install-recommends -y mercurial bzr
RUN mkdir -p /goroot /gopath
ENV GOROOT /goroot
ENV GOPATH /gopath
ENV PATH $PATH:$GOROOT/bin:$GOPATH/bin
RUN curl https://storage.googleapis.com/golang/go1.4.2.linux-amd64.tar.gz | tar xvzf - -C /goroot --strip-components=1
