FROM ubuntu:18.04

RUN apt-get update && apt-get install -y \
    build-essential \
    curl \
    git \
    wget \
    libjpeg-dev \
    openjdk-8-jdk \
    gcc-7 \
    g++-7 \
    zlib1g-dev \
    zlib1g-dev \
    unzip \
    python \
    bash-completion \
    && rm -rf /var/lib/lists/*

RUN curl -L -s https://github.com/bazelbuild/bazel/releases/latest \
| grep -o -m 1 "/bazelbuild.*/bazel_.*-linux-x86_64.deb" \
| awk '{print "https://github.com"$1}' \
| xargs -L 1 curl -L -s > bazel.deb

RUN dpkg -i bazel.deb

# Install Anaconda
WORKDIR /
RUN wget "https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh" -O "miniconda.sh" && \
    bash "miniconda.sh" -b -p "/conda" && \
    rm miniconda.sh && \
    echo PATH='/conda/bin:$PATH' >> /root/.bashrc && \
    /conda/bin/conda config --add channels conda-forge && \
    /conda/bin/conda update --yes -n base conda && \
    /conda/bin/conda update --all --yes

COPY build.sh /build.sh
COPY cuda.sh /cuda.sh

CMD bash build.sh
