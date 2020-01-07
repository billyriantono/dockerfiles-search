ARG GCC_VERSION=6

FROM ma00/lx-gcc:${GCC_VERSION}

ARG CMAKE_VERSION=3.15.5
ARG NINJA_VERSION=1.9.0

WORKDIR /tmp
USER root

RUN export NINJA_URL=https://github.com/ninja-build/ninja/releases/download/v${NINJA_VERSION}/ninja-linux.zip && \
    wget --no-check-certificate --quiet ${NINJA_URL} && \
    unzip -o ninja-linux.zip -d /usr/local/bin && \
    rm ninja-linux.zip

RUN export CMAKE_VERSION_MAJOR=$(echo $CMAKE_VERSION | cut -d. -f1,2) && \
    export CMAKE_URL=https://cmake.org/files/v${CMAKE_VERSION_MAJOR}/cmake-${CMAKE_VERSION}-Linux-x86_64.tar.gz && \
    wget --no-check-certificate --quiet --output-document - ${CMAKE_URL} | \
    tar --strip-components=1 --extract --gzip --directory /usr/local

RUN apt update && \
    apt install --yes \
        bc \
        doxygen \
        freeglut3-dev \
        libarchive-dev \
        libdbus-1-dev \
        libdrm-dev \
        libfontconfig1-dev \
        libgl1-mesa-dev \
        libgles2-mesa-dev \
        libglu1-mesa-dev \
        libgstreamer-plugins-base1.0-0 \
        libgstreamer-plugins-base1.0-dev \
        libgstreamer1.0-0 \
        libgstreamer1.0-dev \
        libjpeg-dev \
        libssl-dev \
        libwayland-dev \
        libxcb-glx0-dev \
        libxcb-icccm4-dev \
        libxcb-image0-dev \
        libxcb-keysyms1-dev \
        libxcb-randr0-dev \
        libxcb-render-util0-dev \
        libxcb-shape0-dev \
        libxcb-shm0-dev \
        libxcb-sync-dev \
        libxcb-xfixes0-dev \
        libxcb-xinerama0-dev \
        libxcb1-dev \
        libxcomposite-dev \
        libxrender-dev \
        libyaml-dev \
        mesa-common-dev \
        mesa-utils \
        openssl \
        python3-click \
        python-dev \
        python3-dev \
        python3-jinja2 \
        python3-path \
        python3-yaml \
        virtualenv \
        zlib1g-dev \
    && \
    pip3 --trusted-host pypi.org --trusted-host files.pythonhosted.org install antlr4-python3-runtime && \
    rm --force --recursive /var/lib/apt/lists/*

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF && \
    echo "deb https://download.mono-project.com/repo/ubuntu xenial/snapshots/5.12.0.301 main" > /etc/apt/sources.list.d/mono-official-5.12.list && \
    apt update && \
    apt install --yes \
        mono-complete && \
    rm --force --recursive /var/lib/apt/lists/*




ARG PROJECT_BASE=/opt/project
ARG PROJECT_NAME=project

WORKDIR ${PROJECT_BASE}
COPY env.sh .

ENV CCACHE_DIR=${PROJECT_BASE}/ccache
ENV CCACHE_BASEDIR=${PROJECT_BASE}/${PROJECT_NAME}
ENV CCACHE_LOGFILE=${PROJECT_BASE}/build/ccache.log
ENV CCACHE_COMPILERCHECK=mtime
ENV CCACHE_CPP2=true
ENV CCACHE_DEPEND=true
ENV CCACHE_MAXSIZE=15G
ENV CCACHE_NOHARDLINK=true
ENV CCACHE_NOHASHDIR=true
ENV CCACHE_SLOPPINESS=file_stat_matches,include_file_mtime,include_file_ctime,file_macro,time_macros

ENV CC='ccache gcc'
ENV CXX='ccache g++'
ENV LANGUAGE=C.UTF-8
ENV LANG=C.UTF-8
ENV LC_ALL=C.UTF-8
ENV PROJECT=${PROJECT_BASE}/${PROJECT_NAME}

CMD [ "/bin/bash" ]

LABEL \
    name=lx-compile \
    maintainer="off@boun.cr" \
    osRelease="Ubuntu 16.04 Xenial" \
    version=2.5
