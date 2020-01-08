FROM ubuntu:14.04

# Let's start with some basic stuff.
RUN apt-get update -qq && apt-get install -qqy \
    apt-transport-https \
    ca-certificates \
    curl \
    wget \
    lxc \
    zip \
    iptables \
    openjdk-7-jre

# Install Apache2
RUN apt-get update \
    && apt-get install -y apache2 \
    libapache2-mod-proxy-html \
    libxml2-dev

# Install Java8
RUN apt-get update \
    && apt-get install -y software-properties-common python-software-properties \
    && add-apt-repository -y ppa:webupd8team/java \
    && echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections \
    && apt-get update \
    && apt-get install -y oracle-java8-set-default

# Install Jenkins
RUN wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | apt-key add - \
    && echo "deb http://pkg.jenkins-ci.org/debian binary/" > /etc/apt/sources.list.d/jenkins.list \
    && apt-get update \
    && apt-get install -y jenkins

# Give sudo permission
RUN echo "jenkins ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers.d/jenkins \
    && chmod 0440 /etc/sudoers.d/jenkins

# Install Docker from Docker Inc. repositories.
ADD asset/docker-engine_1.11.0.deb /docker-engine.deb
RUN apt-get install -y \
    libsystemd-journal0 \
    && dpkg -i docker-engine.deb

# Install the magic wrapper.
ADD start.sh /start.sh
ADD asset/wrapdocker /usr/local/bin/wrapdocker
ADD asset/jenkins_setting /jenkins_setting/
ADD asset/install_jenkins_plugin.sh /install_jenkins_plugin.sh
ADD asset/proxy.conf /proxy.conf
ADD asset/index.html /tmp/index.html
ADD asset/U2Tester.hpi /tmp/U2Tester.hpi
ADD asset/resource /tmp/assets
RUN chmod +x /usr/local/bin/wrapdocker \
    && chmod 755 /start.sh \
    && chmod 755 /install_jenkins_plugin.sh

# Setup environment variables
ENV TIME_ZONE default

EXPOSE 80

VOLUME /jenkins

CMD ["/start.sh"]

