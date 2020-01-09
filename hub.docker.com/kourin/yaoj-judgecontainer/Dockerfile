FROM coreos/apache
RUN \
    apt-get update && \
    apt-get install -y wget curl git apt-file && \
    apt-file update && \
    apt-file search add-apt-repository && \
    apt-get install -y software-properties-common && \
    apt-get install -y python-software-properties && \
    # C/C++
    apt-get install -y build-essential make && \
    add-apt-repository -y ppa:ubuntu-toolchain-r/test && \
    apt-get update && \
    apt-get install -y gcc-5 g++-5 && \
    update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 60 --slave /usr/bin/g++ g++ /usr/bin/g++-5 && \
    # Python3.6
    apt-get install -y zlib1g-dev libssl-dev \
        libreadline-dev libsqlite3-dev libbz2-dev \
        libncurses5-dev libgdbm-dev liblzma-dev \
        tk-dev zlibc && \
    cd /usr/local/src && \
    wget --no-check-certificate https://www.python.org/ftp/python/3.6.3/Python-3.6.3.tgz && \
    tar zxvf Python-3.6.3.tgz && \
    cd Python-3.6.3 && \
    ./configure && \
    make && \
    make altinstall && \
    cd ~ && \
    curl -kL https://bootstrap.pypa.io/get-pip.py | python3.6
WORKDIR /app/ 