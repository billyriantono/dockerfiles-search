FROM yttty/ubuntu-vim-ycm-sshd:latest
LABEL Terrill Yang <terrillyang@gmail.com>

# get dependencies
RUN apt-get update \
    && apt-get install -y build-essential git-core m4 scons zlib1g zlib1g-dev libprotobuf-dev protobuf-compiler libprotoc-dev libgoogle-perftools-dev swig python-dev python python-six \
    && apt-get clean

# checkout repo with mercurial
WORKDIR /usr/local/src
RUN git clone https://github.com/gem5/gem5.git

# build it
WORKDIR /usr/local/src/gem5
ADD build.sh /usr/local/src/gem5/build.sh
RUN chmod ugo+x build.sh \
    && sh build.sh
