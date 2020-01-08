FROM runmymind/docker-android-sdk:latest

# Installing build tools
RUN apt-get update && \
  apt-get install -y \
  build-essential \
  ruby2.3 \
  ruby2.3-dev

# Installing fastlane
RUN gem install fastlane

# Install gradle
RUN wget https://services.gradle.org/distributions/gradle-4.5.1-bin.zip
RUN mkdir /opt/gradle
RUN unzip -d /opt/gradle gradle-4.5.1-bin.zip
RUN export PATH=$PATH:/opt/gradle/gradle-3.4.1/bin

# Work directory
WORKDIR /app