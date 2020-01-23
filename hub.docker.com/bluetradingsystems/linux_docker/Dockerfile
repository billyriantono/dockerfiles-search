FROM ubuntu:bionic


RUN apt-get update && \
DEBIAN_FRONTEND=noninteractive apt-get install -y gnupg wget 

RUN \
echo "deb http://apt.llvm.org/bionic/ llvm-toolchain-bionic-9 main" >> /etc/apt/sources.list && \
wget -O - https://apt.llvm.org/llvm-snapshot.gpg.key > llvm_key && apt-key add llvm_key

RUN \
apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
 libllvm-9-ocaml-dev libllvm9 llvm-9 llvm-9-dev llvm-9-doc llvm-9-examples llvm-9-runtime \
 clang-9 clang-tools-9 clang-9-doc libclang-common-9-dev libclang-9-dev libclang1-9 clang-format-9 python-clang-9 clangd-9 \
 libfuzzer-9-dev \
 lldb-9 \
 lld-9 \
 libc++-9-dev libc++abi-9-dev \
 autoconf \
 automake \
 bsdmainutils \
 cmake \
 curl \
 libunwind8 \
 flex \
 bison \
 autopoint \
 gettext \
 g++ \
 gcc \
 gdb \
 git \
 glibc-source \
 htop  \
 iputils-ping \
 libc6-dbg \
 liblttng-ust-dev \
 libncurses5-dev \
 libreadline-dev \
 libtool \
 libz-dev \
 locales \
 lttng-modules-dkms \
 lttng-tools \
 make \
 nano \
 net-tools \
 ninja-build \
 openssh-server \
 pkg-config \
 python-pip \
 screen \
 silversearcher-ag \
 sudo \
 tcl \
 tcsh \
 texinfo \
 tmux \
 tree \
 unzip \
 uuid-dev \
 vim \
 tcpdump \
 valgrind \
 tzdata \
 npm \
 nodejs \
 rsync \
 datamash \
 hwloc \
 strace \
 sshpass \
 libssh2-1-dev \
 # temporary mono dependency until .net core 2.1
 mono-runtime \
 libfsharp-core4.3-cil \
 libmono-system-net-http4.0-cil \
 mono-reference-assemblies-4.0 \
 bash-completion \
 libpq-dev \
 libpqxx-dev \
 zip \
 && rm -rf /var/lig/apt/lists/*


run \
update-alternatives --install /usr/bin/clang++ clang++ /usr/bin/clang++-9 100; \
update-alternatives --install /usr/bin/clang clang /usr/bin/clang-9 100; \
update-alternatives --config clang; \
update-alternatives --config clang++

# this is done here so that ccache sees clang++ installed, not clang-9
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y ccache 


run pip install pybars3 paramiko mkdocs
run npm install -g npx

# fix locale so we can run tmux
run sed -i 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen
ENV LANG='en_US.utf8' LANGUAGE='en_US:en' LC_ALL='en_US.utf8' TZ='America/Chicago'
run locale-gen

# expand libc sources
run cd /usr/src/glibc ; tar xvf glibc-*.tar.xz

# build cgdb (the version shipped with ubuntu is too old)
copy cgdb-0.7.0.tar.gz /externals/
run cd /externals/ && tar -xvzf cgdb-0.7.0.tar.gz && cd cgdb-0.7.0 && ./configure && make -j$(nproc) && make install

# setup ssh
RUN mkdir /var/run/sshd && echo 'root:root' | chpasswd && \
sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config
# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

# vim friendlier defaults
RUN echo 'set background=dark \n\
set showcmd \n\
set showmatch \n\
set ignorecase \n\
set smartcase \n\
set incsearch \n\
set autowrite \n\
set hidden \n\
set mouse= \n\
imap jj <Esc> \n\
' >> /etc/vim/vimrc

# region NETCORE
# for netcore2 reference https://hub.docker.com/_/microsoft-dotnet-core-sdk
# for netcore3 reference https://github.com/dotnet/dotnet-docker/blob/master/3.0/sdk/bionic/amd64/Dockerfile
# taken from https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/install

RUN wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb \
    && sudo dpkg -i packages-microsoft-prod.deb \
    && sudo apt-get update \
    && sudo apt-get install apt-transport-https -y \
    && sudo apt-get update \
    && sudo apt-get install dotnet-sdk-2.1 -y \
    && sudo apt-get install dotnet-sdk-3.1 -y

# Enable detection of running in a container
ENV DOTNET_RUNNING_IN_CONTAINER=true \
    # Enable correct mode for dotnet watch (only mode supported in a container)
    DOTNET_USE_POLLING_FILE_WATCHER=true \
    # Skip extraction of XML docs - generally not useful within an image/container - helps performance
    NUGET_XMLDOC_MODE=skip
	
# Trigger first run experience by running arbitrary cmd
RUN dotnet help

# Install PowerShell global tool
ENV POWERSHELL_VERSION=7.0.0-preview.4 \
    POWERSHELL_DISTRIBUTION_CHANNEL=PSDocker-DotnetCoreSDK-Ubuntu-18.04

RUN curl -SL --output PowerShell.Linux.x64.$POWERSHELL_VERSION.nupkg https://pwshtool.blob.core.windows.net/tool/$POWERSHELL_VERSION/PowerShell.Linux.x64.$POWERSHELL_VERSION.nupkg \
    && powershell_sha512='0fb0167e13560371bffec38a4a87bf39377fa1a5cc39b3a078ddec8803212bede73e5821861036ba5c345bd55c74703134c9b55c49385f87dae9e2de9239f5d9' \
    && echo "$powershell_sha512  PowerShell.Linux.x64.$POWERSHELL_VERSION.nupkg" | sha512sum -c - \
    && mkdir -p /usr/share/powershell \
    && dotnet tool install --add-source / --tool-path /usr/share/powershell --version $POWERSHELL_VERSION PowerShell.Linux.x64 \
    && rm PowerShell.Linux.x64.$POWERSHELL_VERSION.nupkg \
    && ln -s /usr/share/powershell/pwsh /usr/bin/pwsh \
    # To reduce image size, remove the copy nupkg that nuget keeps.
    && find /usr/share/powershell -print | grep -i '.*[.]nupkg$' | xargs rm	

#vsdbg for remote .net core debugging	
RUN wget https://aka.ms/getvsdbgsh -O - 2>/dev/null | /bin/sh /dev/stdin -v latest -l ~/vsdbg
	
# endregion NETCORE

run DOTNET_SKIP_FIRST_TIME_EXPERIENCE=1 dotnet tool install --tool-path /usr/local/bin paket 
run chmod +X /usr/local/bin/paket

copy sqlite-version-3.26.0.zip extension-functions.c build_sqlite.sh /
run ./build_sqlite.sh && rm -rf /sqlite-version-3.26.0/


#git-lfs
copy git-lfs /usr/bin/
run chmod +x /usr/bin/git-lfs && git lfs install

##### Onload Stuff #####

# Onload version and its md5sum
ARG ONLOAD_VERSION="201811-u1"
ARG ONLOAD_MD5SUM="357e64862aa4145e49d218fd04e63407"

# When ONLOAD_WITHZF is non-empty, the build includes Solarflare's TCPDirect library.
# Default is to exclude it.
ARG ONLOAD_WITHZF

# 1) Install OpenOnload build dependencies
# 2) Download and verify OpenOnload from Solarflare's site
# 3) Extract, build, and install onload
# 4) Cleanup

RUN \
    DEBIAN_FRONTEND=noninteractive apt-get update -y \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        ethtool \
        gcc-multilib \
        libc6-dev-i386 \
        libpcap0.8-dev \
        libtool-bin \
    && cd /tmp \
    && curl -fSL https://www.openonload.org/download/openonload-${ONLOAD_VERSION}.tgz -o /tmp/openonload-${ONLOAD_VERSION}.tgz \
    && echo "${ONLOAD_MD5SUM} openonload-${ONLOAD_VERSION}.tgz" | md5sum --check \
    && tar -zxf openonload-${ONLOAD_VERSION}.tgz \
    && cd /tmp/openonload-${ONLOAD_VERSION} \
    && cd scripts \
    && ./onload_build --user \
    && ./onload_install --userfiles --nobuild \
    && cd /tmp \
    && rm -rf openonload-${ONLOAD_VERSION}.tgz openonload-${ONLOAD_VERSION} \
    && if [ -z ${ONLOAD_WITHZF} ] ; then rm -rf /usr/include/zf /usr/bin/zf_stackdump /usr/bin/zf_debug /usr/lib/x86_64-linux-gnu/zf /usr/lib/x86_64-linux-gnu/libonload_zf* ; fi \
    && DEBIAN_FRONTEND=noninteractive apt-get remove -y --purge \
        curl \
        patch \
    && DEBIAN_FRONTEND=noninteractive apt-get autoremove -y

########################
