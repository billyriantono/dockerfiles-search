FROM frolvlad/alpine-glibc:alpine-3.5_glibc-2.24

RUN apk --no-cache add openjdk8 openssh git ca-certificates wget

ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk
ENV PATH $PATH:/usr/lib/jvm/java-1.8-openjdk/jre/bin:/usr/lib/jvm/java-1.8-openjdk/bin

RUN ssh-keygen -A

RUN mkdir /var/run/sshd \
&& adduser -S -h /home/jenkins -s /bin/sh jenkins && echo "jenkins:jenkins" | chpasswd \
&& sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

RUN echo 'export JAVA_HOME=/usr/lib/jvm/java-1.8-openjdk'  >> /home/jenkins/.profile \
&& echo 'export PATH=$JAVA_HOME/bin:$PATH:/usr/lib/jvm/java-1.8-openjdk/jre/bin:/usr/lib/jvm/java-1.8-openjdk/bin'  >> /home/jenkins/.profile

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]