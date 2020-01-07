FROM ubuntu:16.04
	
RUN set -eux; \
    apt-get update && apt-get -y install \
        bc \
        build-essential \
        chrpath \
        cpio \
        curl \
        debianutils \
        diffstat \
        gawk \
        gcc-multilib \
        git-core \
        iputils-ping \
        libegl1-mesa \
        libsdl1.2-dev \
        locales \
        python \
        python3 \
        python3-git \
        python3-jinja2 \
        python3-pexpect \
        python3-pip \
	python3-chardet \
        screen \
        socat \
        subversion \
        tar \
        texinfo \
        tmux \
        tree \
        unzip \
        vim \
        wget \
        xterm \
        xz-utils \
        zip \
        sudo \
        openjdk-8-jdk-headless \
        ca-certificates \
        p11-kit \
        fontconfig \
        libfreetype6 \
        ;\
    curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends git-lfs && \
    git lfs install && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    locale-gen en_US.UTF-8 && \
    update-locale LANG=en_US.UTF-8

RUN echo "LC_ALL=en_US.UTF-8" >> /etc/environment
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen
RUN echo "LANG=en_US.UTF-8" > /etc/locale.conf
ENV LANG en_US.UTF-8

ENV JQ_VERSION='1.5'
RUN wget --no-check-certificate https://raw.githubusercontent.com/stedolan/jq/master/sig/jq-release.key -O /tmp/jq-release.key && \
    wget --no-check-certificate https://raw.githubusercontent.com/stedolan/jq/master/sig/v${JQ_VERSION}/jq-linux64.asc -O /tmp/jq-linux64.asc && \
    wget --no-check-certificate https://github.com/stedolan/jq/releases/download/jq-${JQ_VERSION}/jq-linux64 -O /tmp/jq-linux64 && \
    gpg --import /tmp/jq-release.key && \
    gpg --verify /tmp/jq-linux64.asc /tmp/jq-linux64 && \
    cp /tmp/jq-linux64 /usr/bin/jq && \
    chmod +x /usr/bin/jq && \
    rm -f /tmp/jq-release.key && \
    rm -f /tmp/jq-linux64.asc && \
    rm -f /tmp/jq-linux64

ENV GRADLE_HOME /opt/gradle
ENV KOTLIN_HOME /opt/kotlinc
ENV ANDROID_HOME "/opt/android_sdk"

# download and install Gradle
# https://services.gradle.org/distributions/
ARG GRADLE_VERSION=5.2.1
RUN cd /opt && \
    wget -q https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip && \
    unzip gradle*.zip && \
    ls -d */ | sed 's/\/*$//g' | xargs -I{} mv {} gradle && \
    rm gradle*.zip

# download and install Kotlin compiler
# https://github.com/JetBrains/kotlin/releases/latest
ARG KOTLIN_VERSION=1.3.41
RUN cd /opt && \
    wget -q https://github.com/JetBrains/kotlin/releases/download/v${KOTLIN_VERSION}/kotlin-compiler-${KOTLIN_VERSION}.zip && \
    unzip *kotlin*.zip && \
    rm *kotlin*.zip

# Android sdk
ENV VERSION_SDK_TOOLS "4333796"

RUN curl -s https://dl.google.com/android/repository/sdk-tools-linux-${VERSION_SDK_TOOLS}.zip > /sdk.zip && \
    unzip /sdk.zip -d ${ANDROID_HOME} && \
    rm -v /sdk.zip

RUN mkdir -p $ANDROID_HOME/licenses/ \
  && echo "8933bad161af4178b1185d1a37fbf41ea5269c55\nd56f5187479451eabf01fb78af6dfcb131a6481e" > $ANDROID_HOME/licenses/android-sdk-license \
  && echo "84831b9409646a918e30573bab4c9c91346d8abd" > $ANDROID_HOME/licenses/android-sdk-preview-license

RUN yes | $ANDROID_HOME/tools/bin/sdkmanager "platforms;android-28"

ENV PATH ${PATH}:${GRADLE_HOME}/bin:${KOTLIN_HOME}/bin:${ANDROID_HOME}/tools:${ANDROID_HOME}/tools/bin

# add user to sudoers after sudo is installed
RUN useradd --create-home --home-dir /home/build --uid 1000 --gid 100 --shell /bin/bash build && \
    echo "build ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers; \
    adduser build sudo

RUN chown -R build ${ANDROID_HOME}

# download dumb-init after curl has been installed
# RUN wget -O /bin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v1.2.2/dumb-init_1.2.2_amd64 --no-check-certificate && \
#    chmod +x /bin/dumb-init
  
#ENTRYPOINT ["/bin/dumb-init", "-v", "--"]
CMD ["/bin/bash"]

USER build
WORKDIR /home/build
