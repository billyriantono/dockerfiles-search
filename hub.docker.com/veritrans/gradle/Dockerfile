# Pull base image.
FROM veritrans/jdk:oracle-jdk8

# disable interactive functions
ENV DEBIAN_FRONTEND noninteractive

# Install Java
RUN apt-get update && \
  apt-get dist-upgrade -y && \
  apt-get -y install unzip && \
  wget 'https://services.gradle.org/distributions/gradle-2.14-bin.zip' -O /tmp/gradle-2.14-bin.zip && \
  unzip -d /usr/local/ /tmp/gradle-2.14-bin.zip && \
  ln -s /usr/local/gradle-2.14/bin/gradle /usr/bin/gradle && \
  rm -f /tmp/gradle-2.14-bin.zip && \
  apt-get purge -y --auto-remove unzip && \
  apt-get clean


# Define working directory.
WORKDIR /data

# Define commonly used JAVA_HOME variable
ENV GRADLE_HOME /usr/local/gradle-2.14

# Define default command.
CMD ["bash"]

