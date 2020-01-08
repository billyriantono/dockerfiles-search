FROM isuper/java-oracle:jre_8

LABEL Description="Ubuntu 16.04 + Java + SSHD"

MAINTAINER Devis Lucato "https://github.com/dluc/docker-ubuntu-java-sshd"

# To use this image, you must accept the Oracle Binary Code License Agreement for Java SE
# http://www.oracle.com/technetwork/java/javase/terms/license/index.html

RUN apt-get update && \
    apt-get install -y --no-install-recommends openssh-server && \
    mkdir /var/run/sshd && \
    echo 'root:root' |chpasswd && \
    sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config && \
    apt-get clean

EXPOSE 22

CMD    ["/usr/sbin/sshd", "-D"]
