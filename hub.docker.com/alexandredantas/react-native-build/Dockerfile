FROM ubuntu:18.04

ENV JAVA_HOME=/opt/zulu8.38.0.13-ca-jdk8.0.212-linux_x64 \ 
    PATH=/opt/zulu8.38.0.13-ca-jdk8.0.212-linux_x64/bin:$PATH \
    ANDROID_HOME=/opt/android \
    TZ=America/Sao_Paulo

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone && \
  cd /opt && \
  apt-get update && \
  apt-get install -y curl gnupg2 apt-transport-https unzip && \
  curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
  echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
  curl -sL https://deb.nodesource.com/setup_12.x | bash - && \
  apt-get update && \
  apt-get install -y git openssh-client nodejs yarn awscli && \
  curl -o sdktools.zip https://dl.google.com/android/repository/sdk-tools-linux-4333796.zip && \
  curl -o jdk.tgz https://cdn.azul.com/zulu/bin/zulu8.38.0.13-ca-jdk8.0.212-linux_x64.tar.gz && \
  tar -xf jdk.tgz && \
  unzip -q sdktools.zip && \
  rm -f jdk.tgz sdktools.zip && \
  export JAVA_HOME=/opt/zulu8.38.0.13-ca-jdk8.0.212-linux_x64 && \
  export PATH=$JAVA_HOME/bin:$PATH && \
  mkdir /opt/android && \
  mv /opt/tools /opt/android && \
  yes | /opt/android/tools/bin/sdkmanager --licenses && \
  /opt/android/tools/bin/sdkmanager "platform-tools"


