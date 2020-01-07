FROM buildpack-deps:jessie-scm
ENV GO_VERSION 1.5.1
ENV GO_DOWNLOAD_URL https://storage.googleapis.com/golang/go1.5.1.linux-amd64.tar.gz
ENV GOLANG_DOWNLOAD_SHA1 46eecd290d8803887dec718c691cc243f2175fe0
ENV GOPATH /opt/docker/packages/golang
ENV GOROOT /opt/docker/packages/goroot
ENV PATH $PATH:$GOPATH/bin
ENV PATH $PATH:$GOROOT/bin
ADD docker-entrypoint.sh /entrypoint.sh
VOLUME ["/opt/docker/packages/golang/", "/opt/docker/packages/goroot/"]
ENTRYPOINT ["/entrypoint.sh"]
