FROM selenium/standalone-firefox:latest
LABEL authors=Desjardins

USER root

RUN rm -rf /var/lib/apt/lists/*
RUN export TERM=xterm-color
RUN apt-get update && apt-get install -y apt-transport-https
RUN apt-get -y install software-properties-common
RUN add-apt-repository -y ppa:webupd8team/java # access the Oracle Java repository
RUN apt-get -y install openjdk-8-jdk # install the JDK version 8
RUN apt-get -y install daemon
RUN chmod +x /opt/bin/entry_point.sh
RUN daemon --name="selenium-server-daemon" -b ~/daemon.out -l ~/daemon.err -v -- /opt/bin/entry_point.sh