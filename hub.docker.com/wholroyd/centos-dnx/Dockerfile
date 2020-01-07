FROM wholroyd/centos-nodejs:latest

MAINTAINER William Holroyd <wholroyd@gmail.com>

ENV DNX_VERSION 1.0.0-beta6
ENV DNX_USER_HOME /opt/dnx
ENV PATH $PATH:$DNX_USER_HOME/runtimes/default/bin

## Install the Mono environment

# https://github.com/aspnet/dnx/issues/1590
ENV MONO_THREADS_PER_CPU 2000

RUN rpm --import "http://keyserver.ubuntu.com/pks/lookup?op=get&search=0x3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF"
RUN yum install -y yum-utils

RUN yum-config-manager --add-repo http://download.mono-project.com/repo/centos/
RUN yum -y install mono-devel ca-certificates-mono fsharp mono-vbnc nuget unzip

# Make Mono trust SSL certificates
RUN mozroots --import --sync

## Install libuv for Kestrel from source code

RUN yum -y install \
    make \
    autoconf \
    automake \
    build-essential \
    libtool
    
RUN LIBUV_VERSION=1.4.2 && \
    curl -sSL https://github.com/libuv/libuv/archive/v${LIBUV_VERSION}.tar.gz | tar zxfv - -C /usr/local/src && \
    cd /usr/local/src/libuv-$LIBUV_VERSION && \
    sh autogen.sh && ./configure && make && make install && \
    rm -rf /usr/local/src/libuv-$LIBUV_VERSION && \
    ldconfig
    
# https://github.com/aspnet/Home/issues/760
RUN ln -s /usr/local/lib/libuv.so /usr/lib && \
    ln -s /usr/local/lib/libuv.so.1 /usr/lib && \
    ln -s /usr/local/lib/libuv.so /usr/lib64 && \
    ln -s /usr/local/lib/libuv.so.1 /usr/lib64
    
## Installs the DNX environment

RUN curl -sSL https://raw.githubusercontent.com/aspnet/Home/dev/dnvminstall.sh | DNX_USER_HOME=$DNX_USER_HOME DNX_BRANCH=v$DNX_VERSION sh
RUN bash -c "source $DNX_USER_HOME/dnvm/dnvm.sh && \
    dnvm install $DNX_VERSION -a default && \
    dnvm alias default | xargs -i ln -s $DNX_USER_HOME/runtimes/{} $DNX_USER_HOME/runtimes/default"

WORKDIR /data

# Define default command.
CMD ["bash"]
