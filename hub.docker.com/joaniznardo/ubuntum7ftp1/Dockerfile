## partim d'una nova base per poder generar la imatge de manera automàtica: automated builds

#FROM ubuntu:14.04
FROM joaniznardo/ubuntum7base

MAINTAINER joaniznardo (github)

#RUN apt-get update && apt-get install -y tcpdump inotify-tools openssh-server sudo supervisor
#RUN useradd -m ubuntu && echo "ubuntu:ubuntu" | chpasswd && adduser ubuntu sudo

RUN echo "proftpd-basic shared/proftpd/inetd_or_standalone select standalone" | debconf-set-selections && apt-get install -y proftpd

#CMD /etc/init.d/ssh restart && supervisord -n
