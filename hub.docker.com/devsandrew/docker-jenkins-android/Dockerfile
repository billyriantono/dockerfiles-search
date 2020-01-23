FROM ubuntu:18.04

# Install timezone
ENV TZ=Europe/Kiev
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Add i386 architecture
RUN dpkg --add-architecture i386

# Update packages
RUN apt-get update && apt-get install -y git \
 wget \
 unzip \
 sudo \
 tzdata \
 locales\
 openjdk-8-jdk \
 libncurses5:i386 \
 libstdc++6:i386 \
 zlib1g:i386 \
 curl

# Clear to reduce image size
RUN apt-get clean && rm -rf /var/lib/apt/lists /var/cache/apt

# Set locales
RUN locale-gen en_US.UTF-8  
ENV LANG en_US.UTF-8  
ENV LANGUAGE en_US:en  
ENV LC_ALL en_US.UTF-8

# Download and unpack
ARG android_home_dir=/var/lib/android-sdk/
ARG sdk_tools_zip_file=sdk-tools-linux-4333796.zip
RUN mkdir $android_home_dir
RUN wget https://dl.google.com/android/repository/$sdk_tools_zip_file -P $android_home_dir -nv
RUN unzip $android_home_dir$sdk_tools_zip_file -d $android_home_dir
RUN rm $android_home_dir$sdk_tools_zip_file && chmod 777 -R $android_home_dir

# Install environment
ENV ANDROID_HOME=$android_home_dir
ENV PATH="${PATH}:$android_home_dir/tools/bin:$android_home_dir/platform-tools"
ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/

# Agree with licenses Android SDK
RUN yes | sdkmanager --licenses

# Create a working directory for Jenkins
ENV JENKINS_HOME=/var/lib/jenkins
RUN mkdir $JENKINS_HOME && chmod 777 $JENKINS_HOME

# Create a new user with the name jenkins, make him superuser, switch to it and go to the working directory
RUN useradd -m jenkins && echo 'jenkins ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
USER jenkins
WORKDIR /home/jenkins

# Load and run the war file with the latest version Jenkins
RUN wget http://mirrors.jenkins.io/war-stable/latest/jenkins.war -nv
CMD java -jar jenkins.war

# Install FIrebase
RUN curl -sL firebase.tools | bash

EXPOSE 8080/tcp