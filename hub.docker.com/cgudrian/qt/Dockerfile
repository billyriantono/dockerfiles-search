FROM debian:latest

ARG major=5
ARG minor=9
ARG release=2

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -yq --no-install-recommends \
        git subversion python wget build-essential \
        libfontconfig libdbus-1-3 libx11-6 libx11-xcb1 libglib2.0 libgl1-mesa-glx && \
    rm -rf /var/lib/apt/lists/*

COPY qt-installer-noninteractive.qs /tmp/

RUN wget --no-check-certificate https://download.qt.io/official_releases/qt/${major}.${minor}/${major}.${minor}.${release}/qt-opensource-linux-x64-${major}.${minor}.${release}.run -O /tmp/install.run && \
    chmod +x /tmp/install.run && \
    /tmp/install.run --platform minimal --verbose --script /tmp/qt-installer-noninteractive.qs && \
    rm -rf /tmp/*

ENV PATH="/opt/qt/Tools/QtCreator/bin:/opt/qt/${major}.${minor}.${release}/gcc_64/bin:${PATH}"

RUN qbs setup-toolchains --detect && \
    qbs setup-qt /opt/qt/${major}.${minor}.${release}/gcc_64/bin/qmake qt${major}${minor}${release} && \
    qbs config defaultProfile qt${major}${minor}${release}
