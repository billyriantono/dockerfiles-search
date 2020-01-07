FROM ubuntu:18.04

RUN sed -i "s/^deb /deb \[arch=$(dpkg --print-architecture)] /" /etc/apt/sources.list
RUN for SUFFIX in "" "-updates" "-security"; do \
  echo "deb [arch=armhf] http://ports.ubuntu.com/ubuntu-ports/ xenial${SUFFIX} main restricted universe multiverse" \
    >> /etc/apt/sources.list.d/armhf.list; \
  done

# gcc for cgo
RUN apt-get update && apt-get install -y \
        build-essential \
        autotools-dev \
        libssl-dev \
        dh-autoreconf \
        opensc \
        opensc-pkcs11 \
        g++ \
        gcc \
        libc6-dev \
        make \
        cmake \
        curl \
        libpcre3-dev \
        git \
        sudo \
        gcc-arm-linux-gnueabihf \
        g++-arm-linux-gnueabihf \
        libusb++-dev \
        libssh2-1 \
	sudo

# Add the google cloud sdk. This will allow child containers to push to google cloud repositories
RUN echo "deb http://packages.cloud.google.com/apt cloud-sdk-xenial main" | tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
    apt-get update -y && apt-get install google-cloud-sdk -y


RUN mkdir /tmp/swig/
COPY swig.tar.gz /tmp/swig/
RUN tar -C /tmp/swig/ --strip-components=1 -xzf /tmp/swig/swig.tar.gz \
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

ENV GOLANG_VERSION 1.13.34
WORKDIR /home/developer/
COPY go1.10.3.linux-amd64.tar.gz /home/developer/golang.tar.gz

RUN  tar -C /home/developer/ -xzf golang.tar.gz \
	&& rm golang.tar.gz

ENV GOROOT /home/developer/go
ENV GOPATH /home/developer/
ENV PATH $GOROOT/bin:$PATH

WORKDIR $GOPATH

CMD /bin/bash
