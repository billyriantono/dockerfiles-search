FROM ubuntu:trusty
MAINTAINER wangzhijiebill@gmail.com
RUN apt-get update
RUN apt-get dist-upgrade -y
RUN export DEBIAN_FRONTEND=noninteractive
RUN apt-get -y dist-upgrade
RUN apt-get -y install python-software-properties
RUN apt-get -y install software-properties-common
RUN apt-get -y install git
RUN apt-get install -y openssh-server
RUN sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd
RUN mkdir -p /var/run/sshd
EXPOSE 22



# Add user jenkins to the image
RUN adduser --quiet jenkins
# Set password for the jenkins user (you may want to alter this).
RUN echo "jenkins:jenkins" | chpasswd
# Install Java.
RUN \
  echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  add-apt-repository -y ppa:webupd8team/java && \
  apt-get update && \
  apt-get install -y oracle-java8-installer && \
  rm -rf /var/lib/apt/lists/* && \
  rm -rf /var/cache/oracle-jdk8-installer
# Define working directory.
WORKDIR /data

# Define commonly used JAVA_HOME variable
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle

# Define default command.
# GOOGLE ADNROID SDK source http://dl.google.com/android/android-sdk_r24.4.1-linux.tgz
# ADD android-sdk_r24.4.1-linux.tgz /opt/android
RUN mkdir /opt/android
ADD http://dl.google.com/android/android-sdk_r24.4.1-linux.tgz /opt/android.tgz
RUN tar zxvf /opt/android.tgz -C /opt/android

# DOCKER ADD will automatically unzip
ENV ANDROID_HOME /opt/android/android-sdk-linux
ENV PATH $ANDROID_HOME/bin/:$ANDROID_HOME/platform-tools:$ANDROID_HOME/tools:$ANDROID_HOME:$PATH
RUN cat /etc/environment
RUN echo $ANDROID_HOME
# RUN android
RUN echo "y" | android update sdk --no-ui --all --filter platform-tools-23.0.1,build-tools-23.0.1,android-23,android-22,android-21,android-20,android-19
CMD ["/usr/sbin/sshd", "-D"]
