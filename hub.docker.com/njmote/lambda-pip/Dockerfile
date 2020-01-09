FROM ubuntu

RUN apt-get update && apt-get install -y --no-install-recommends \
        build-essential \
        curl \
        dos2unix \
        libfreetype6-dev \
        libpng12-dev \
        libzmq3-dev \
        nano \
        pkg-config \
        python \
        python-dev \
        python3 \
        python3-dev \
        python3-pip \
        rsync \
        software-properties-common \
        unzip \
        zip \
        && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN curl -O https://bootstrap.pypa.io/get-pip.py && \
    python get-pip.py && \
    rm get-pip.py

RUN pip install --upgrade pip

RUN mkdir /working

WORKDIR /working

ADD src/pip-and-zip.sh /bin/pip-and-zip.sh

RUN dos2unix /bin/pip-and-zip.sh

RUN chmod +x /bin/pip-and-zip.sh

CMD . /bin/pip-and-zip.sh