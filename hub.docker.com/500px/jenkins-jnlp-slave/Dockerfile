FROM cloudbees/java-build-tools

USER root

RUN apt-get update -qqy \
  && apt-get -qqy --no-install-recommends install \
    python-pip \
    python-dev \
    libffi-dev \
    libssl-dev \
    libxml2-dev \
    libxslt1-dev \
    libjpeg8-dev \
    zlib1g-dev \
    libyaml-dev \
  && rm -rf /var/lib/apt/lists/*

RUN pip install \
  ansible==1.9.4 \
  dnspython==1.12.0 \
  netaddr==0.7.18

RUN curl --create-dirs -sSLo /usr/share/jenkins/slave.jar http://repo.jenkins-ci.org/public/org/jenkins-ci/main/remoting/2.59/remoting-2.59.jar \
  && chmod 755 /usr/share/jenkins \
  && chmod 644 /usr/share/jenkins/slave.jar

COPY jenkins-slave /usr/local/bin/jenkins-slave

RUN chmod a+rwx /home/jenkins
WORKDIR /home/jenkins
USER jenkins

ENTRYPOINT ["/opt/bin/entry_point.sh", "/usr/local/bin/jenkins-slave"]
