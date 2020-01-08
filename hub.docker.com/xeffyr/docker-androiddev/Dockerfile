##
## Build with:
##   docker build -t xeffyr/docker-androiddev .
##
## Push to docker hub with:
##   docker push xeffyr/docker-androiddev:latest
##

FROM ubuntu:19.04

ENV ANDROID_SDK_REVISION "4333796"
ENV ANDROID_SDK_BUILD_TOOLS_VERSION "29.0.2"
ENV ANDROID_NDK_VERSION "20.0.5594570"
ENV ANDROID_STUDIO_VERSION "3.5.2.0"
ENV ANDROID_STUDIO_BUILD_NUMBER "191.5977832"
ENV ANDROID_HOME "/opt/android/sdk"
ENV NDK "/opt/android/sdk/ndk/${ANDROID_NDK_VERSION}"
ENV LANG en_US.UTF-8

# Needed for installing some 32bit packages.
RUN dpkg --add-architecture i386

# Install essential packages.
RUN apt update && env DEBIAN_FRONTEND=noninteractive apt upgrade -yq && \
    env DEBIAN_FRONTEND=noninteractive apt install -yq --no-install-recommends \
    apktool \
    asciidoc \
    asciidoctor \
    autoconf \
    automake \
    autopoint \
    bison \
    bsdmainutils \
    curl \
    docbook-to-man \
    docbook-utils \
    ed \
    elixir \
    erlang-nox \
    flex \
    gawk \
    gettext \
    git \
    g++ \
    g++-multilib \
    gnome-common \
    gnupg \
    gobject-introspection \
    gperf \
    groff \
    gtk-3-examples \
    gtk-doc-tools \
    help2man \
    intltool \
    itstool \
    jq \
    libc-ares-dev \
    libexpat1-dev \
    libdbus-1-dev \
    libffi-dev \
    libgc-dev \
    libgdk-pixbuf2.0-dev \
    libgirepository1.0-dev \
    libgl1 \
    libglib2.0-dev \
    libgmp-dev \
    libgtk-3-bin \
    libicu-dev \
    libisl-dev \
    libjpeg-dev \
    libltdl-dev \
    libmpc-dev \
    libmpfr-dev \
    libncurses5-dev \
    libncursesw5-dev \
    libpulse0 \
    libsigsegv-dev \
    libssl-dev \
    libtool-bin \
    libunistring-dev \
    libwayland-dev \
    llvm-8-tools \
    locales \
    lua5.3 \
    lzip \
    m4 \
    openjdk-8-jdk-headless \
    pandoc \
    pax-utils \
    pkg-config \
    python3.7 \
    python3.8 \
    python3-docutils \
    python3-pip \
    python3-recommonmark \
    python3-setuptools \
    python3-sphinx \
    python-pip \
    python-rdflib \
    python-setuptools \
    python-xcbgen \
    python-yaml \
    rsync \
    ruby \
    scons \
    texinfo \
    unzip \
    valac \
    xfonts-utils \
    xutils-dev \
    xmlto \
    zip \
    zlib1g-dev

# Install 32bit packages.
RUN env DEBIAN_FRONTEND=noninteractive apt install -yq --no-install-recommends \
    libssl-dev:i386 \
    zlib1g-dev:i386

# Install additional developer tools.
RUN env DEBIAN_FRONTEND=noninteractive apt install -yq --no-install-recommends \
    nano \
    silversearcher-ag \
    patchelf \
    patchutils

# These packages are unneeded.
RUN env DEBIAN_FRONTEND=noninteractive apt purge -yq \
    openjdk-11-jre-headless || true

# Configure locales.
RUN locale-gen --purge en_US.UTF-8 && \
    echo -e 'LANG="en_US.UTF-8"\nLANGUAGE="en_US:en"\n' > /etc/default/locale

# Install configuration files.
COPY ./conf/etc/nanorc /etc/nanorc
RUN chmod 644 /etc/nanorc

# Custom shell profile.
RUN echo "export PATH=\"${PATH}:${ANDROID_HOME}/tools/bin:${ANDROID_HOME}/tools:${ANDROID_HOME}/platform-tools\"" > /etc/profile.d/androiddev.sh && \
    chmod 644 /etc/profile.d/androiddev.sh && \
    echo "alias cp='cp -i'" >> /etc/bash.bashrc && \
    echo "alias ln='ln -i'" >> /etc/bash.bashrc && \
    echo "alias mv='mv -i'" >> /etc/bash.bashrc && \
    echo "alias rm='rm -i'" >> /etc/bash.bashrc && \
    echo "alias egrep='egrep --color=auto'" >> /etc/bash.bashrc && \
    echo "alias fgrep='fgrep --color=auto'" >> /etc/bash.bashrc && \
    echo "alias grep='grep --color=auto'" >> /etc/bash.bashrc && \
    echo "alias ls='ls --color=auto'" >> /etc/bash.bashrc && \
    echo "alias l.='ls --color=auto -d .*'" >> /etc/bash.bashrc && \
    echo "alias la='ls --color=auto -a'" >> /etc/bash.bashrc && \
    echo "alias ll='ls --color=auto -Fhl'" >> /etc/bash.bashrc && \
    echo "alias ll.='ls --color=auto -Fhl -d .*'" >> /etc/bash.bashrc && \
    echo "alias dir='dir --color=auto'" >> /etc/bash.bashrc && \
    echo "alias vdir='vdir --color=auto -h'" >> /etc/bash.bashrc

# Create user and add it to sudoers.
RUN env DEBIAN_FRONTEND=noninteractive apt install -yq --no-install-recommends sudo && \
    useradd -U -m -s /bin/bash builder && \
    echo "builder ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/builder

# Create necessary directories.
RUN mkdir /data && chown builder:builder /data && \
    mkdir -p /opt/android && chown builder:builder /opt/android

# Switch to normal user.
USER builder:builder
WORKDIR /home/builder

# Installing Android SDK.
RUN curl --fail --retry 3 -L -o sdk.zip https://dl.google.com/android/repository/sdk-tools-linux-${ANDROID_SDK_REVISION}.zip && \
    unzip -q sdk.zip -d ${ANDROID_HOME}
RUN mkdir -p ~/.android && echo 'count=0' > ~/.android/repositories.cfg
RUN echo y | $ANDROID_HOME/tools/bin/sdkmanager "platform-tools"
RUN echo y | $ANDROID_HOME/tools/bin/sdkmanager "build-tools;${ANDROID_SDK_BUILD_TOOLS_VERSION}"
RUN echo y | $ANDROID_HOME/tools/bin/sdkmanager "platforms;android-21"
RUN echo y | $ANDROID_HOME/tools/bin/sdkmanager "platforms;android-23"
RUN echo y | $ANDROID_HOME/tools/bin/sdkmanager "platforms;android-24"
RUN echo y | $ANDROID_HOME/tools/bin/sdkmanager "platforms;android-26"
RUN echo y | $ANDROID_HOME/tools/bin/sdkmanager "platforms;android-28"
RUN echo y | $ANDROID_HOME/tools/bin/sdkmanager "platforms;android-29"
RUN echo y | $ANDROID_HOME/tools/bin/sdkmanager "ndk;${ANDROID_NDK_VERSION}"

# Installing Android Studio.
RUN curl --fail --retry 3 -L -o studio.tar.gz https://dl.google.com/dl/android/studio/ide-zips/${ANDROID_STUDIO_VERSION}/android-studio-ide-${ANDROID_STUDIO_BUILD_NUMBER}-linux.tar.gz && \
    tar zxf studio.tar.gz && mv android-studio /opt/android/studio

# Cleanup.
RUN sudo apt-get clean && \
    sudo rm -rf /var/lib/apt/lists/*
