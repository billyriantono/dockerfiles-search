FROM google/cloud-sdk

ENV VERSION=1.9
ENV OS=linux
ENV ARCH=amd64
ENV PATH=$PATH:/usr/local/go/bin
ENV PATH=$PATH:/usr/local/gomon
ENV GOPATH=/go

COPY gomon /usr/local/bin/gomon

RUN curl -O https://dl.google.com/go/go$VERSION.$OS-$ARCH.tar.gz
RUN tar -C /usr/local -xzf go$VERSION.$OS-$ARCH.tar.gz
RUN rm go$VERSION.$OS-$ARCH.tar.gz

CMD ["tail", "-f", "/dev/null"]