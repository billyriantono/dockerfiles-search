FROM jstarcher/jenkins-slave-ubuntu
MAINTAINER Jordan Starcher <jstarcher@gmail.com>

RUN apt-get update && \
    apt-get install -y fabric && \
    apt-get clean

CMD ["/usr/sbin/sshd", "-D"]
