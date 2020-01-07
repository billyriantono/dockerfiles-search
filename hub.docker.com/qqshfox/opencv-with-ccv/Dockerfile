FROM qqshfox/opencv:latest
MAINTAINER Hanfei Shen <qqshfox@gmail.com>

ENV CCV_VERSION unstable
RUN mkdir -p /src && \
    curl -sSL https://github.com/liuliu/ccv/archive/$CCV_VERSION.tar.gz | tar -xzC /src && \
    ln -s /src/ccv-$CCV_VERSION /src/ccv && \
    cd /src/ccv/lib && \
    sed -ri 's/^MKCFLAGS="(.*)"$/MKCFLAGS="\1 -fPIC "/' configure && \
    ./configure && \
    make
