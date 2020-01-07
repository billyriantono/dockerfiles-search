FROM ubuntu:16.04
RUN mkdir /install
ADD . /install 
WORKDIR /install
ENV HOME=/install
RUN apt-get update -y && apt-get  install software-properties-common apt-transport-https -y

#install neovim
RUN add-apt-repository ppa:neovim-ppa/unstable -y
RUN apt-get update -y && apt-get install -y git zsh \
 curl \
 neovim \
 python3-dev \
 python3-pip \
 python-dev \
 python-pip \
 wget \
 haproxy \
 libffi-dev \
 libssl-dev \
 libxml2-dev \
 libxslt1-dev \
 libjpeg8-dev \
 zlib1g-dev \
 silversearcher-ag

RUN curl -O https://bootstrap.pypa.io/get-pip.py && \
    python3 get-pip.py && \
    python get-pip.py && \
    rm get-pip.py

ENV TERM=xterm-256color

# install buttefly
RUN pip install butterfly supervisor libsass

#install fuzzy search
RUN wget https://github.com/jhawthorn/fzy/releases/download/0.7/fzy_0.7-1_amd64.deb; exit 0
RUN dpkg -i fzy_0.7-1_amd64.deb

# install golang 
RUN wget https://storage.googleapis.com/golang/go1.7.1.linux-amd64.tar.gz
RUN tar -C /usr/local -xzf go1.7.1.linux-amd64.tar.gz
ENV GOPATH=/root
ENV PATH=$PATH:/usr/local/go/bin:$GOPATH/bin

# install ansible
RUN sh install_ansible.sh

WORKDIR /
ENV HOME=/root
RUN rm -rf install

#install texlive
RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        libfreetype6-dev \
        libpng12-dev \
        libzmq3-dev \
        pkg-config \
        python-dev \
        git \
    	httpie \
	curl \
	liblapack-dev \
	libatlas-dev \
        python-dev \
        gfortran \	
        rsync \
        unzip \
        pandoc \
        texlive-full && \  
        apt-get clean && \
        rm -rf /var/lib/apt/lists/*

WORKDIR /tmp


WORKDIR /
	
