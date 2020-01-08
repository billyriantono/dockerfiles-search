FROM truevolve/android_headless_builder

# gcc for cgo
RUN apt-get update && apt-get install -y \
		g++ \
		gcc \
		libc6-dev \
		make \
		curl \
		libpcre3-dev \
		vim \
		git \
		sudo

RUN curl -kfsSL https://excellmedia.dl.sourceforge.net/project/swig/swig/swig-3.0.12/swig-3.0.12.tar.gz -o swig.tar.gz \
	&& mkdir /tmp/swig/ \
	&& tar -C /tmp/swig/ --strip-components=1 -xzf swig.tar.gz \
	&& cd /tmp/swig/ \
	&& ./configure \
	&& make \
	&& make install

RUN mkdir -p /home/developer/ && \
    echo "developer:x:1000:1000:Developer,,,:/home/developer:/bin/bash" >> /etc/passwd && \
    echo "developer:x:1000:" >> /etc/group && \
    echo "developer ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/developer && \
    chmod 0440 /etc/sudoers.d/developer && \
    chown developer:developer -R /home/developer

USER developer

ENV GOLANG_VERSION 1.12.5
ENV GOLANG_DOWNLOAD_URL https://golang.org/dl/go$GOLANG_VERSION.linux-amd64.tar.gz

WORKDIR /home/developer/
RUN curl -kfsSL "$GOLANG_DOWNLOAD_URL" -o golang.tar.gz \
	&& tar -C /home/developer/ -xzf golang.tar.gz \
	&& rm golang.tar.gz

ENV GOROOT /home/developer/go
ENV GOPATH /home/developer/
ENV PATH $GOROOT/bin:$GOPATH/bin:$PATH
WORKDIR $GOPATH

RUN go get golang.org/x/tools/go/packages && go get golang.org/x/mobile/cmd/gomobile && gomobile init

CMD /bin/bash
