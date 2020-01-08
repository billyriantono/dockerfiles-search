FROM ubuntu:16.04

# Install java8
RUN apt-get update && \
  apt-get install -y software-properties-common && \
  add-apt-repository -y ppa:webupd8team/java && \
  (echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections) && \
  apt-get update && \
  apt-get install -y oracle-java8-installer && \
  apt-get clean && \
  rm -fr /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install Deps
RUN dpkg --add-architecture i386 && apt-get update && apt-get install -y --force-yes expect git wget libc6-i386 lib32stdc++6 lib32gcc1 lib32ncurses5 lib32z1 python curl libqt5widgets5 && apt-get clean && rm -fr /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install Android SDK
ENV VERSION_SDK_TOOLS=3952940 \
	  ANDROID_HOME=/usr/local/android-sdk-linux
ENV	PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/tools/bin:$ANDROID_HOME/platform-tools
RUN apt-get update && apt-get install unzip && \
    mkdir -p $ANDROID_HOME && \
    chown -R root.root $ANDROID_HOME && \
    wget -q -O sdk.zip http://dl.google.com/android/repository/sdk-tools-linux-$VERSION_SDK_TOOLS.zip && \
    unzip sdk.zip -d $ANDROID_HOME && \
    rm -f sdk.zip
RUN echo $ANDROID_HOME
RUN mkdir -p /root/.android && \
    touch /root/.android/repositories.cfg
    
RUN yes | sdkmanager --licenses && sdkmanager --update

RUN yes | sdkmanager \
  "tools" \
  "platform-tools" \
  "build-tools;28.0.3" \
  "extras;android;m2repository" \
  "platforms;android-28" \
  "extras;google;m2repository"

# Setup environment variables
ENV JAVA8_HOME /usr/lib/jvm/java-8-oracle
RUN echo "export JAVA_HOME=$JAVA8_HOME" | cat - ~/.bashrc >> temp && mv temp ~/.bashrc && \
    echo "export JAVA8_HOME=$JAVA8_HOME" | cat - ~/.bashrc >> temp && mv temp ~/.bashrc && \
    echo "export ANDROID_HOME=$ANDROID_HOME" | cat - ~/.bashrc >> temp && mv temp ~/.bashrc

# Setup ssh server
RUN apt-get update && \
  apt-get install -y openssh-server && \
  mkdir /var/run/sshd && \
  echo 'root:root' |chpasswd && \
  sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config && \
  sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
EXPOSE 22
CMD    ["/usr/sbin/sshd", "-D"]

# Cleaning
RUN apt-get clean