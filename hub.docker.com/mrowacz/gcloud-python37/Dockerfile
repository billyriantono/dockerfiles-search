FROM google/cloud-sdk:237.0.0

RUN apt update && apt upgrade -y
RUN apt install -qqy \
        build-essential \
        checkinstall \
        libreadline-gplv2-dev \
        libncursesw5-dev \
        libssl-dev \
        libsqlite3-dev \
        tk-dev \
        libgdbm-dev \
        libc6-dev \
        libbz2-dev \
        zlib1g \
        wget

RUN apt install -qqy \
        libffi-dev

WORKDIR '/usr/src/'
RUN wget https://www.python.org/ftp/python/3.7.2/Python-3.7.2.tgz
RUN tar xzf Python-3.7.2.tgz
WORKDIR '/usr/src/Python-3.7.2'
RUN ./configure --enable-optimizations
RUN make altinstall
WORKDIR '/'
RUN rm -rf /usr/src/Python-3.7.2
RUN rm /usr/src/Python-3.7.2.tgz