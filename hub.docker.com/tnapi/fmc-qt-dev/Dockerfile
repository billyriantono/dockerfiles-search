# Inspired by: https://github.com/garthk/qt-build/blob/bionic-5.12.0/Dockerfile

FROM ubuntu:bionic

ARG QT=5.12.3
ARG QTM=5.12
ARG QTSHA=b72eeec96bef4daf14abf38a0f3f37748d7e483a706c59263a8129632fea98aa
ARG QTCOMPONENTS=gcc_64
ARG DELETE="Docs Examples MaintenanceTool /tmp/qt/installer.run /tmp/qt/script.qs"
ARG QMATRIXCLIENT=0.5.1.2

RUN apt-get update -q && \
    DEBIAN_FRONTEND=noninteractive apt-get install -q -y --no-install-recommends \
        ca-certificates \
        libfontconfig1 \
        libice6 \
        libsm6 \
        libx11-xcb1 \
        libxext6 \
        libxrender1 \
        p7zip \
        xvfb \
        build-essential \
        cmake \
        git-core \
        libpulse0 \
        libpulse-mainloop-glib0 \
        locales \
        dbus \
        libxcb-xinerama0 \
        libglib2.0-0 \
        libxkbcommon-x11-0 \
        libgl1-mesa-dev \
        gdb \
        clang-format \
        wget \
    && apt-get clean

# Run qt installer

ARG QTRUNFILE=http://download.qt.io/official_releases/qt/${QTM}/${QT}/qt-opensource-linux-x64-${QT}.run

# Steps, kicking off from the tail end of installerdeps above:
ADD qt-installer-noninteractive.qs /tmp/qt/script.qs
ENV QTM=$QTM
ENV QTSHA=$QTSHA
ENV QTCOMPONENTS=$QTCOMPONENTS
ENV DELETE=$DELETE

# use bash for RUN until the next FROM, so we can use bash strict mode
# http://redsymbol.net/articles/unofficial-bash-strict-mode/
SHELL ["/bin/bash", "-c"]
RUN set -euo pipefail \
    && wget -O /tmp/qt/installer.run ${QTRUNFILE} \
    && echo "${QTSHA}  /tmp/qt/installer.run" | sha256sum -c \
    && chmod +x /tmp/qt/installer.run \
    && xvfb-run -e /dev/stderr /tmp/qt/installer.run --script /tmp/qt/script.qs --verbose \
    && rm -rf /tmp/qt \
    && cd /opt/qt \
    && rm -rf ${DELETE}

RUN for COMPONENT in `echo ${QTCOMPONENTS} | tr , ' '`; do echo /opt/qt/${QT}/${COMPONENT}/lib >> /etc/ld.so.conf.d/qt-${QT}.conf; done
RUN locale-gen en_US.UTF-8 && DEBIAN_FRONTEND=noninteractive dpkg-reconfigure locales
ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/opt/qt/${QT}/gcc_64/bin

# Install libQMatrixClient

SHELL ["/bin/bash", "-c"]
RUN set -euo pipefail \
    && cd ~ \
    && git clone --single-branch --branch ${QMATRIXCLIENT} https://github.com/QMatrixClient/libqmatrixclient.git \
    && mkdir -p ~/libqmatrixclient/build_dir \
    && cd ~/libqmatrixclient/build_dir \
    && cmake -DQMATRIXCLIENT_INSTALL_EXAMPLE=OFF .. \
    && cmake --build . --target install \
    && rm -rf ~/libqmatrixclient



# The rest can be left to the default:
ARG VCS_REF
ARG BUILD_DATE

LABEL org.label-schema.build-date="$BUILD_DATE" \
      org.label-schema.name="fmc-docker-qt-dev" \
      org.label-schema.description="Qt $QT build environment" \
      org.label-schema.url="e.g. https://bitbucket.org:federatedmissioncontrol/fmc-docker-qt-dev" \
      org.label-schema.vcs-ref="$VCS_REF" \
      org.label-schema.vcs-url="https://bitbucket.org:federatedmissioncontrol/fmc-docker-qt-dev.git" \
      org.label-schema.version="$QT" \
      org.label-schema.schema-version="1.0"


