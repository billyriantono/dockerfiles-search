FROM ivantichy/oracle-java8

RUN apt-get update && apt-get install -y -q apt-transport-https ca-certificates && apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D && \
echo "deb https://apt.dockerproject.org/repo debian-jessie main" >> /etc/apt/sources.list.d/docker.list && \
apt-get update -y && \
apt-get install fail2ban -y -q && \
apt-get install git -y -q && \
apt-get install sudo -y -q && \
apt-get install maven -y -q && \
apt-get install iptables -y -q && \
apt-get install openvpn -y -q && \
apt-get install -y -q openssh-server && \
apt-get install -y -q curl wget  && \
apt-get install -y -q inotify-tools  && \
sudo apt-get install -y -q docker-engine && \
rm -rf /var/lib/apt/lists/*

RUN sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd
RUN mkdir -p /var/run/sshd

RUN useradd -d /home/java -m -s /bin/bash java
RUN useradd -d /home/jenkins -m -s /bin/bash jenkins

RUN echo "jenkins ALL=(java) NOPASSWD: /bin/bash" >> /etc/sudoers
RUN echo "jenkins ALL=(root) NOPASSWD: /bin/su - java" >> /etc/sudoers

RUN echo "jenkins ALL=(ALL:ALL) NOPASSWD:ALL" >> /etc/sudoers

RUN echo "nobody    ALL=(ALL:ALL) NOPASSWD: /sbin/route" >> /etc/sudoers
RUN echo "java    ALL=(ALL:ALL) NOPASSWD: /sbin/iptables, /sbin/iptables-save, /sbin/iptables-restore /etc/iptables/rules.v4.backup" >> /etc/sudoers

RUN chown -R java:java /etc/openvpn/ && mkdir -p /etc/iptables/ && chown -R java:java /etc/iptables/

# Set password for the jenkins user (you may want to alter this).
RUN echo "jenkins:jenkins" | chpasswd

COPY ./runme.sh ./runme.sh

RUN chmod +x ./runme.sh

# Standard SSH port
EXPOSE 22

ENTRYPOINT ["./runme.sh"]
