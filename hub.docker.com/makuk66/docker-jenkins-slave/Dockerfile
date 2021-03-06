# This Dockerfile is used to build an image containing basic stuff to be used as a Jenkins slave build node,
# plus dependencies for our build and some python tools we use for testing.
# Note the plaintext password here; depending on your environment that may not be advisable.
# Based on evarga/jenkins-slave
FROM    makuk66/docker-oracle-java7
MAINTAINER  Martijn Koster "mak-docker@greenhills.co.uk"

ENV PHANTOMJS_VERSION=1.9.8

ADD requirements.txt /tmp/requirements.txt

RUN export DEBIAN_FRONTEND=noninteractive && \
  apt-get update && \
  apt-get -y install ant git openssh-server \
  build-essential libxml2-dev libxslt1-dev python-dev python-pip \
  curl netcat-openbsd net-tools procps lsof && \
  sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd && \
  mkdir -p /var/run/sshd && \
  adduser --quiet --gecos "" --disabled-password jenkins && \
  (echo "jenkins:jenkins" | chpasswd)  && \
  apt-get -y install libmysqlclient-dev && \
  pip install virtualenv && \
  pip install -r /tmp/requirements.txt && \
  rm /tmp/requirements.txt && \
  wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-$PHANTOMJS_VERSION-linux-x86_64.tar.bz2 && \
  apt-get -y install bzip2 libfreetype6 libfontconfig && \
  tar xjC /opt < phantomjs-$PHANTOMJS_VERSION-linux-x86_64.tar.bz2 && \
  rm phantomjs-$PHANTOMJS_VERSION-linux-x86_64.tar.bz2 && \
  ln -s /opt/phantomjs-$PHANTOMJS_VERSION-linux-x86_64/bin/phantomjs /usr/local/bin/ && \
  apt-get -y install vim && \
  apt-get -y install smbclient
RUN wget -qO- https://get.docker.com/ | sh && \
  usermod -aG docker jenkins

EXPOSE 22 8764

CMD ["/usr/sbin/sshd", "-D"]
