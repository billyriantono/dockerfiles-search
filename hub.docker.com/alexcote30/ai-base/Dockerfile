FROM ubuntu:latest

USER root
WORKDIR /opt

# Linux packages
RUN DEBIAN_FRONTEND=noninteractive apt update -y && apt upgrade -y
RUN DEBIAN_FRONTEND=noninteractive apt install -y --fix-missing --no-install-recommends \
    build-essential \
    cmake \
    git \
    locales \
    nano \
    pkg-config \
    python3-dev \
    python3-numpy \
    python3-pip \
    python3-setuptools \
    telnet \
    unzip \
    wget \
    tzdata \
    zip \
    zlib1g-dev && \
    apt autoremove -y && \
    apt clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Locales
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    dpkg-reconfigure --frontend=noninteractive locales && \
    update-locale LANG=en_US.UTF-8
ENV LANG en_US.UTF-8 

# Python packages
RUN DEBIAN_FRONTEND=noninteractive apt update -y && apt upgrade -y
RUN pip3 install --upgrade pip
RUN git clone https://github.com/facebookresearch/fastText.git && pip3 install ./fastText
RUN pip3 install \
    argparse \
    awscli \  
    c3pyo \
    dateparser \
    face_recognition \
    flask \
    fuzzywuzzy \
    gevent \
    gunicorn \
    nano \
    nltk \
    numpy \
    pandas \
    pyeda \
    python-Levenshtein \
    psycopg2-binary \
    requests \
    scikit-learn \
    slackclient \
    torch \
    torchvision \
    tqdm \
    unidecode \
    wheel
RUN python3 -c 'import nltk; nltk.download("punkt")'
RUN python3 -c 'import nltk; nltk.download("vader_lexicon")'
RUN python3 -c 'import nltk; nltk.download("wordnet")'
RUN python3 -c 'import nltk; nltk.download("stopwords")'

# Faiss
RUN apt install -y --fix-missing --no-install-recommends \
    build-essential \
    libblas-dev \
    liblapack-dev \
    swig && \
    apt autoremove -y && \
    apt clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
RUN git clone https://github.com/facebookresearch/faiss.git && \
    cd faiss && \
    ./configure && make && make install && \
    sed -i 's/PYTHONCFLAGS =  -I/PYTHONCFLAGS =  -I\/usr\/include\/python3.6m\/ -I\/usr\/lib\/python3\/dist-packages\/numpy\/core\/include/' makefile.inc && \
    cd /opt/faiss && \
    make -i py && \
    pip3 install ./python/ && \
    cd / && \
    python3 -c "import faiss"

# Docker user
RUN groupadd -r dockeruser -g 433 && \
    useradd -u 431 -r -g dockeruser -d /opt/ -s /sbin/nologin -c "Docker User" dockeruser && \
    chown -R dockeruser:dockeruser /opt/

USER dockeruser
CMD tail -f /dev/null
