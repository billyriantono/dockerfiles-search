# docker run -e TEAMCITY_SERVER=http://buildserver:8111 -dt -p 9090:9090 juanpablo/centos7-teamcity-agent-android-23

FROM ariya/centos7-oracle-jre7

MAINTAINER Juan Prado <juan@juanpabloprado.com>

ADD setup-agent.sh /setup-agent.sh
RUN yum -y install wget unzip sudo
RUN adduser teamcity

RUN wget -qO- http://dl.google.com/android/android-sdk_r24.4.1-linux.tgz | tar xz -C /opt
ENV ANDROID_HOME /opt/android-sdk-linux
ENV PATH $PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools
RUN echo y | android update sdk --no-ui --all --filter tools,platform-tools,build-tools-23.0.1,android-23,extra-google-m2repository,extra-google-google_play_services,extra-android-support

EXPOSE 9090
CMD sudo -u teamcity -s -- sh -c "TEAMCITY_SERVER=$TEAMCITY_SERVER bash /setup-agent.sh run"