FROM ubuntu:16.04

ENV SDK_TOOLS "3859397"
ENV ANDROID_HOME "/opt/sdk"


RUN apt-get update
RUN echo y | apt-get install wget curl unzip default-jdk python-software-properties
RUN curl -sL https://deb.nodesource.com/setup_8.x -o nodesource_setup.sh && bash nodesource_setup.sh && apt-get install nodejs

RUN dpkg --add-architecture i386
RUN apt-get -qqy update
RUN apt-get -qqy install libncurses5:i386 libstdc++6:i386 zlib1g:i386

# Download and extract Android Tools
RUN wget http://dl.google.com/android/repository/sdk-tools-linux-${SDK_TOOLS}.zip -O /tmp/tools.zip && \
	mkdir -p ${ANDROID_HOME} && \
	unzip /tmp/tools.zip -d ${ANDROID_HOME} && \
	rm -v /tmp/tools.zip

ENV PATH /opt/sdk/tools/bin:$PATH

# Configure Android
RUN mkdir -p ${ANDROID_HOME}/licenses/ && \
    yes | sdkmanager --licenses && \
	mkdir -p /root/.android/ && touch /root/.android/repositories.cfg

RUN curl https://sdk.cloud.google.com | bash

ENV PATH /google-cloud-sdk/bin:$PATH

COPY google-cloud-auth.sh /google-cloud-auth.sh
RUN chmod u+x /google-cloud-auth.sh

VOLUME ["/.config"]

CMD ["/bin/bash","/google-cloud-auth.sh"]
