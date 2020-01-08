From java:8
MAINTAINER Jimmy Yang <gankkank@gmail.com>

RUN \
  apt-get update && \
  DEBIAN_FRONTEND=noninteractive apt-get install -y openssh-server locales


# SSH
RUN mkdir /var/run/sshd
# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd
ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile


RUN apt-get update && \
  apt-get install -y \
  mongodb-clients \
  postgresql-client \
  redis-tools \
  vim sudo \
  rsync \
  python-pip 

RUN pip install awscli

# Clean up
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN useradd -u 1000 -d /var/jenkins_home -m jenkins

RUN echo "jenkins ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/jenkins


# Handle locale
RUN echo "en_US.UTF-8 UTF-8" > /etc/locale.gen
RUN locale-gen
RUN update-locale
ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8

RUN \
  curl -o /bin/gosu -sSL "https://github.com/tianon/gosu/releases/download/1.4/gosu-$(dpkg --print-architecture)" \
  && chmod +x /bin/gosu

COPY docker-entrypoint.sh /entrypoint.sh

ENV JENKINS_PASS=jenkins_pass
RUN echo "jenkins:$JENKINS_PASS" | chpasswd

RUN mkdir /var/jenkins_home/.ssh
RUN chown -R jenkins:jenkins /var/jenkins_home

RUN chmod 755 /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
