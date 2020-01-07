FROM octohost/base:trusty

ENV GO_VERSION=1.7.5

RUN curl -sf -o /tmp/go${GO_VERSION}.linux-amd64.tar.gz -L https://storage.googleapis.com/golang/go${GO_VERSION}.linux-amd64.tar.gz; \
  mkdir -p /opt && cd /opt && tar xfz /tmp/go${GO_VERSION}.linux-amd64.tar.gz && rm -f /tmp/go${GO_VERSION}.linux-amd64.tar.gz

ENV GOROOT /opt/go
ENV GOPATH /root/gocode
ENV PATH /opt/go/bin:/root/gocode/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
