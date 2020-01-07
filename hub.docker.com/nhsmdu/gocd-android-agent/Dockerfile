FROM gocd/gocd-agent-ubuntu-16.04:v18.6.0

RUN apt-get update \
 && apt-get upgrade -y \
 && apt-get install wget libssl-dev openjdk-8-jdk maven -y \
 && curl -sL "https://deb.nodesource.com/setup_8.x" | bash - \
 && apt-get install nodejs -y \
 && groupadd --gid 1001 node \
 && useradd --uid 1001 --gid node --shell /bin/bash --create-home node

# workaround for issue https://github.com/angular/angular-cli/issues/7389
USER node
RUN mkdir /home/node/.npm-global
ENV PATH=/home/node/.npm-global/bin:$PATH
ENV NPM_CONFIG_PREFIX=/home/node/.npm-global
RUN npm i -g sonarqube-scanner@2.0.2

USER go

# Gradle
RUN mkdir ~/gradle \
 && cd ~/gradle \
 && wget -nv https://services.gradle.org/distributions/gradle-4.5.1-bin.zip \
 && unzip gradle-4.5.1-bin.zip

# download android sdk
RUN mkdir ~/android-sdk-linux \
 && cd ~/android-sdk-linux \
 && wget -nv https://dl.google.com/android/repository/sdk-tools-linux-3859397.zip \
 && unzip sdk-tools-linux-3859397.zip \
 && cd ~/android-sdk-linux/tools \
 && yes | bin/sdkmanager --licenses \
 && bin/sdkmanager --update

RUN cd ~/android-sdk-linux/tools \
 && bin/sdkmanager "platform-tools" "platforms;android-23" "platforms;android-24" "platforms;android-25" "platforms;android-26" "platforms;android-27"

# Really, REALLY make sure that Go Agent listens to what I want the path to be set to
RUN echo 'export PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/home/go/gradle/gradle-4.5.1/bin:/home/go/android-sdk-linux/platform-tools:/home/go/android-sdk-linux/tools"' >> ~/.profile \
 && echo 'export ANDROID_HOME="/home/go/android-sdk-linux"' >> ~/.profile
RUN echo 'export PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/home/go/gradle/gradle-4.5.1/bin:/home/go/android-sdk-linux/platform-tools:/home/go/android-sdk-linux/tools"' >> ~/.bashrc \
 && echo 'export ANDROID_HOME="/home/go/android-sdk-linux"' >> ~/.bashrc

USER root

#RUN echo 'PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/home/go/gradle/gradle-4.5.1/bin:/home/go/android-sdk-linux/platform-tools:/home/go/android-sdk-linux/tools"' >> /etc/environment \
# && echo 'ANDROID_HOME="/home/go/android-sdk-linux"' >> /etc/environment
#
#RUN echo 'export PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/home/go/gradle/gradle-4.5.1/bin:/home/go/android-sdk-linux/platform-tools:/home/go/android-sdk-linux/tools"' >> ~/.profile \
# && echo 'export ANDROID_HOME="/home/go/android-sdk-linux"' >> ~/.profile
#RUN echo 'export PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/home/go/gradle/gradle-4.5.1/bin:/home/go/android-sdk-linux/platform-tools:/home/go/android-sdk-linux/tools"' >> ~/.bashrc \
# && echo 'export ANDROID_HOME="/home/go/android-sdk-linux"' >> ~/.bashrc
