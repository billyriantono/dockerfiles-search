FROM ubuntu:14.04


# ------------------------------------------------------
# --- Environments and base directories

# Environments
# - Language
RUN locale-gen en_US.UTF-8
ENV LANG "en_US.UTF-8"
ENV LANGUAGE "en_US.UTF-8"
ENV LC_ALL "en_US.UTF-8"



# ------------------------------------------------------
# --- Install required tools



RUN apt-get update -qq

# Base (non android specific) tools
# -> should be added to bitriseio/docker-bitrise-base

# Dependencies to execute Android builds
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y git curl vim zip wget software-properties-common openjdk-7-jdk libc6-i386 lib32stdc++6 lib32gcc1 lib32ncurses5 lib32z1

# install jdk8
RUN add-apt-repository ppa:openjdk-r/ppa
RUN apt-get update -qq
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes openjdk-8-jdk

# install Ruby from source
#  from source: mainly because of GEM native extensions,
#  this is the most reliable way to use Ruby on Ubuntu if GEM native extensions are required
RUN DEBIAN_FRONTEND=noninteractive apt-get -y install build-essential zlib1g-dev libssl-dev libreadline6-dev libyaml-dev
RUN wget -q http://cache.ruby-lang.org/pub/ruby/ruby-2.3.0.tar.gz
RUN tar -xvzf ruby-2.3.0.tar.gz
RUN cd ruby-2.3.0 && ./configure --disable-install-doc --prefix=/usr/local && make && make install
# cleanup
RUN rm -rf ruby-2.3.0
RUN rm ruby-2.3.0.tar.gz

RUN gem install bundler --no-document

# install fastlane
RUN gem install fastlane

# Install a basic SSH server
RUN apt-get install -y openssh-server
RUN sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd
RUN mkdir -p /var/run/sshd

# Add user jenkins to the image
RUN adduser --quiet jenkins
# Set password for the jenkins user (you may want to alter this).
RUN echo "jenkins:jenkins" | chpasswd

ENV JAVA8_HOME "/usr/lib/jvm/java-1.8.0-openjdk-amd64/"
ENV JAVA_HOME "/usr/lib/jvm/java-1.8.0-openjdk-amd64/"

# Install gcloud for device testing
# Add the Cloud SDK distribution URI as a package source
RUN echo "deb http://packages.cloud.google.com/apt cloud-sdk-$(lsb_release -c -s) main" | tee /etc/apt/sources.list.d/google-cloud-sdk.list

# Import the Google Cloud public key
RUN curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -

# Update and install the Cloud SDK
RUN apt-get update && apt-get install -y google-cloud-sdk

# Install Android
ENV GRADLE_URL http://services.gradle.org/distributions/gradle-2.14.1-all.zip
RUN curl -L ${GRADLE_URL} -o /tmp/gradle-2.14.1-all.zip && unzip /tmp/gradle-2.14.1-all.zip -d /home/gradle && rm /tmp/gradle-2.14.1-all.zip
ENV GRADLE_HOME /home/gradle/gradle-2.14.1

# Download and untar SDK
ENV ANDROID_SDK_URL https://dl.google.com/android/repository/tools_r25.2.3-linux.zip
RUN wget -qO- -O tmp.zip ${ANDROID_SDK_URL} && unzip tmp.zip -d /home/android_sdk && rm tmp.zip
ENV ANDROID_HOME /home/android_sdk

ENV PATH $PATH:${ANDROID_HOME}/tools/bin:${GRADLE_HOME}/bin

RUN chmod -R a+x ${ANDROID_HOME}

# Standard SSH port
EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
