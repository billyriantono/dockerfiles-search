FROM octohost/base:trusty

# Go 1.5.1
RUN curl -sf -o /tmp/go1.5.1.linux-amd64.tar.gz -L https://storage.googleapis.com/golang/go1.5.1.linux-amd64.tar.gz && mkdir -p /opt && cd /opt && tar xfz /tmp/go1.5.1.linux-amd64.tar.gz && rm -f /tmp/go1.5.1.linux-amd64.tar.gz

ENV GOROOT /opt/go
ENV GOPATH /root/gocode
ENV PATH /opt/go/bin:/root/gocode/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
