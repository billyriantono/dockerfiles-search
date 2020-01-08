FROM mysql:5.7
RUN mkdir -p /initialization/python
WORKDIR /initialization/python
RUN apt-get update && apt-get install -y \
    build-essential \
    python3-pip \
    zlib1g-dev \
    libncurses5-dev \
    libgdbm-dev \
    libnss3-dev \
    libssl-dev \
    libreadline-dev \
    libffi-dev \
    curl \
    && curl -O https://www.python.org/ftp/python/3.7.3/Python-3.7.3.tar.xz \
    && tar -xf Python-3.7.3.tar.xz \
    && cd Python-3.7.3 \
    && ./configure --enable-optimizations \
    && make -j 8 \
    && make altinstall \
    && cd .. \
    && python3.7 -m pip install --upgrade pip

RUN apt-get remove -y \
    build-essential \
    zlib1g-dev \
    libncurses5-dev \
    libgdbm-dev \
    libnss3-dev \
    libssl-dev \
    libreadline-dev \
    libffi-dev \
    curl \
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*