# Dockerfile to build TeamCity build agent container images.
# Based on Debian.

# sudo docker run -e TEAMCITY_SERVER=http://buildserver:8111 -dt -p 8222:8222 davidjenni/teamcity-android-agent
# or if the server is running on the same host:
# sudo docker run -e TEAMCITY_SERVER=http://teamcity_server:8111 \
#   --link teamcity_server:teamcity_server -dt davidjenni/teamcity-android-agent

FROM debian:wheezy
ENV ANDROID_VERSION 24.0.2

ADD setup-agent.sh /setup-agent.sh

RUN	apt-get update && \
		apt-get install -y adduser default-jre sudo unzip wget && \
		rm -rf /var/lib/apt/lists/*

RUN wget -qO- http://dl.google.com/android/android-sdk_r$ANDROID_VERSION-linux.tgz | tar xz -C /opt
ENV ANDROID_HOME /opt/android-sdk-linux
ENV PATH $PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools
RUN echo y | android update sdk --filter android-21,tool,platform-tool,build-tools-21.1.2,extra-android-support,extra-android-m2repository --no-ui -a

RUN adduser teamcity

EXPOSE 8222
CMD sudo -u teamcity -s -- sh -c "TEAMCITY_SERVER=$TEAMCITY_SERVER ANDROID_HOME=$ANDROID_HOME PATH=$PATH bash /setup-agent.sh run"
