FROM jenkins/jenkins

ARG BUILD_DATE
ARG VCS_REF
ARG VERSION

LABEL org.label-schema.build-date=$BUILD_DATE \
  org.label-schema.docker.cmd="docker run -d --restart=always --network=host --name=Jenkins --env=TRY_UPGRADE_IF_NO_MARKER=true -v $(readlink -f /var/run/docker.sock):$(readlink -f /var/run/docker.sock) -v $(which docker):$(which docker) -v jenkins_home:/var/jenkins_home dtulyakov/jenkins" \
  org.label-schema.description="Jenkins server" \
  org.label-schema.name="jenkins" \
  org.label-schema.schema-version="2.199" \
  org.label-schema.url="https://jenkins.io/" \
  org.label-schema.vcs-ref=$VCS_REF \
  org.label-schema.vcs-url="https://bitbucket.org/dtulyakov/docker-jenkins" \
  org.label-schema.vendor="dtulyakov" \
  org.label-schema.version=$VERSION

USER root

RUN set -x \
  && apt-get update -qq \
  && apt-get install --no-install-recommends -qy \
     software-properties-common \
     python-requests \
     python3-pip \
     python3-setuptools \
     apt-transport-https \
     ca-certificates \
     curl \
     gnupg2 \
     rsync \
     ruby \
     ruby-dev \
  && pip3 install pip --upgrade \
  && pip install pep8 \
     pylint \
     pytest \
     pytest-cov \
  && apt-add-repository 'deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main' \
  && add-apt-repository 'deb [arch=amd64] https://download.docker.com/linux/debian stretch stable' \
  && apt-key adv --no-tty --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367 \
  && apt-key adv --no-tty --keyserver keyserver.ubuntu.com --recv-keys 7EA0A9C3F273FCD8 \
  && apt-get update -qq \
  && apt-get install -qy ansible docker-ce \
  && apt-get autoremove -y \
  && usermod -aG docker jenkins \
  && rm -fr /var/lib/apt/lists/* /tmp/* /var/tmp/* /var/cache/apt/archives/*

USER jenkins

COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

# Вообще всё это можно поставить на агентах и не трогать основной образ ;)
# Пример запуска `pylint somefile.py`
# Пример запуска `pychecker somefile.py`
# Пример запуска `pep8 somefile.py`
# tox `это` юнит тесты для python
# Если надо поиграться с судо
# RUN apt-get install -y sudo
# RUN echo "jenkins ALL=NOPASSWD: ALL" >> /etc/sudoers

# vim: set filetype=dockerfile et sw=2 ts=2:
