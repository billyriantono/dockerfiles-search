FROM java:8

MAINTAINER Petri Sirkkala <sirpete@iki.fi>

USER root

ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN true

RUN \
  apt-get update && \
  apt-get -y install \
    apt-transport-https \
    build-essential \
    git \
    locales \
    lsb-release \
    maven \
    rsync \
    software-properties-common \
    sudo \
    graphviz \
    jq \
    python-pip && \
  update-alternatives --set java /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java && \
  rm -rf /var/lib/apt/lists/*

# From: https://docs.docker.com/engine/installation/linux/docker-ce/debian/#install-using-the-repository
#==============
# Docker
#=============
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
RUN add-apt-repository \
    "deb [arch=amd64] https://download.docker.com/linux/debian \
    $(lsb_release -cs) \
    stable"
RUN apt-get update && apt-get install -y docker-ce

# From: https://docs.docker.com/compose/install/#install-compose
#==============
# Docker compose
#=============
RUN curl -L https://github.com/docker/compose/releases/download/1.23.2/docker-compose-Linux-x86_64 -o /usr/local/bin/docker-compose
RUN chmod +x /usr/local/bin/docker-compose

RUN pip install awscli --upgrade

# From: https://docs.aws.amazon.com/AmazonECS/latest/developerguide/ECS_CLI_installation.html
#==============
# ecs-cli
#=============
RUN \
  curl -o /usr/local/bin/ecs-cli https://s3.amazonaws.com/amazon-ecs-cli/ecs-cli-linux-amd64-latest && \
  chmod +x /usr/local/bin/ecs-cli

ENV JENKINS_SWARM_VERSION 3.14
ENV HOME /home/jenkins-slave

RUN \
  useradd -c "Jenkins Slave user" -d $HOME -m jenkins-slave && \
  usermod -a -G sudo,docker jenkins-slave && \
  echo "jenkins-slave ALL=(ALL) NOPASSWD:ALL" >/etc/sudoers.d/jenkins-slave && \
  curl --create-dirs -sSLo /usr/share/jenkins/swarm-client-$JENKINS_SWARM_VERSION.jar \
    https://repo.jenkins-ci.org/releases/org/jenkins-ci/plugins/swarm-client/$JENKINS_SWARM_VERSION/swarm-client-$JENKINS_SWARM_VERSION.jar && \
  chmod 755 /usr/share/jenkins

# Set the locale
RUN \
  echo "LANG=en_US.UTF-8" > /etc/default/locale && \
  echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && \
  locale-gen

ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8
ENV JAVA_OPTS -Duser.country=US -Duser.language=en

# Set the timezone
RUN \
  ln -sf /usr/share/zoneinfo/Europe/Helsinki /etc/localtime
ENV TZ Europe/Helsinki

COPY jenkins-slave.sh /usr/local/bin/jenkins-slave.sh
RUN chmod 777 /usr/local/bin/jenkins-slave.sh

VOLUME /home/jenkins-slave

WORKDIR /home/jenkins-slave

USER root

ENTRYPOINT ["/usr/local/bin/jenkins-slave.sh"]
