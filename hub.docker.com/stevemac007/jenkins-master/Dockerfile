FROM jenkinsci/jenkins
MAINTAINER Steve Mactaggart <steve@whitesquaresoft.com>

USER root

RUN apt-get update && apt-get -y dist-upgrade
RUN apt-get install -y python-pip

RUN mkdir -p /var/lib/jenkins/updates/
RUN curl -L https://updates.jenkins-ci.org/update-center.json | sed '1d;$d' > "/var/lib/jenkins/updates/default.json"

RUN /usr/local/bin/install-plugins.sh git ansicolor
RUN /usr/local/bin/install-plugins.sh amazon-ecs
RUN /usr/local/bin/install-plugins.sh bitbucket
RUN /usr/local/bin/install-plugins.sh pipeline-model-definition
RUN /usr/local/bin/install-plugins.sh job-dsl
RUN /usr/local/bin/install-plugins.sh build-pipeline-plugin
RUN /usr/local/bin/install-plugins.sh ansicolor
RUN /usr/local/bin/install-plugins.sh slack
RUN /usr/local/bin/install-plugins.sh ssh-credentials
RUN /usr/local/bin/install-plugins.sh rbenv
RUN /usr/local/bin/install-plugins.sh blueocean
RUN /usr/local/bin/install-plugins.sh envinject
RUN /usr/local/bin/install-plugins.sh jobcacher
RUN /usr/local/bin/install-plugins.sh delivery-pipeline-plugin
RUN /usr/local/bin/install-plugins.sh matrix-auth

RUN pip install bumpversion awscli
RUN pip install jinja2-cli

COPY scripts /usr/local/jenkins/install
RUN mkdir /tmp/jenkins-groovy
COPY groovy/* /tmp/jenkins-groovy/

CMD /usr/local/jenkins/install/entrypoint.sh
