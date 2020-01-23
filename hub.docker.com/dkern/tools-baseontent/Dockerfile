FROM ubuntu:16.04
ADD 100-ubnt.list /etc/apt/sources.list.d/
ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv C0A52C50
RUN apt-get update && apt-get -y upgrade && apt-get -y dist-upgrade
RUN apt-get update && apt-get -y install unifi net-tools supervisor execstack
RUN execstack -c /usr/lib/unifi/lib/native/Linux/amd64/libubnt_webrtc_jni.so
EXPOSE 8080/tcp 8081/tcp 8443/tcp 8843/tcp 8880/tcp 3478/udp
VOLUME ["/usr/lib/unifi/data", "/usr/lib/unifi/logs", "/var/log/supervisor"]
WORKDIR /usr/lib/unifi
CMD ["/usr/bin/supervisord"]
