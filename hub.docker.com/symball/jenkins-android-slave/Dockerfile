FROM debian:jessie

ENV HOME /home/jenkins
ENV ANDROID_VS 24.4.1
ENV BUILD_TOOLS_VS  24.0.2
ENV GRADLE_VS 3.1
ENV ANT_VS 1.9.7

RUN apt-get update && apt-get install -y \
  net-tools \
  openssh-server \
  libc-bin \
  build-essential \
  default-jre-headless \
  default-jdk \
  zlib1g-dev \
  ncurses-dev \
  libx11-dev \
  libxrender1 \
  curl \
  unzip \
  wget \
  git \
  && rm -rf /var/lib/apt/lists/*


# Set SSH Configuration to allow remote logins without /proc write access
RUN sed -i 's|session required pam_loginuid.so|session optional pam_loginuid.so|g' /etc/pam.d/sshd

# Configure a Jenkins User. Needed for the SSH communication
RUN useradd -d $HOME -u 1000 -m -s /bin/bash jenkins
RUN mkdir -p $HOME/.ssh

WORKDIR /usr/local
RUN curl -SL http://dl.google.com/android/android-sdk_r$ANDROID_VS-linux.tgz \
| tar -xz
RUN mv /usr/local/android-sdk-linux /usr/local/android-sdk
RUN curl -SL http://ftp.cuhk.edu.hk/pub/packages/apache.org//ant/binaries/apache-ant-$ANT_VS-bin.tar.gz \
| tar -xz
RUN wget -SL https://services.gradle.org/distributions/gradle-$GRADLE_VS-all.zip && \
unzip -o gradle-$GRADLE_VS-all.zip && rm gradle-$GRADLE_VS-all.zip

# Install Android tools
RUN echo y | /usr/local/android-sdk/tools/android update sdk --no-ui --force --filter \
 tools,platform-tools,android-24,build-tools-24.0.2

# Environment variables
ENV ANDROID_HOME /usr/local/android-sdk
ENV ANT_HOME /usr/local/apache-ant-$ANT_VS
ENV GRADLE_HOME /usr/local/gradle-$GRADLE_VS

# Set path options
ENV PATH $PATH:$ANDROID_HOME/tools
ENV PATH $PATH:$ANDROID_HOME/platform-tools
ENV PATH $PATH:$ANDROID_HOME/build-tools/$BUILD_TOOLS_VS
ENV PATH $PATH:$ANT_HOME/bin
ENV PATH $PATH:$MAVEN_HOME/bin
ENV PATH $PATH:$GRADLE_HOME/bin
