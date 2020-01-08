FROM jenkins

# Add Plugins
RUN mkdir -p /usr/share/jenkins/ref/plugins
RUN cd /usr/share/jenkins/ref/plugins/

USER root
RUN chown -R jenkins /usr/share/jenkins/ref/plugins

RUN curl -O https://updates.jenkins-ci.org/download/plugins/ws-cleanup/latest/ws-cleanup.hpi
RUN curl -O https://updates.jenkins-ci.org/download/plugins/swarm/latest/swarm.hpi
RUN curl -O https://updates.jenkins-ci.org/download/plugins/scm-api/latest/scm-api.hpi
RUN curl -O https://updates.jenkins-ci.org/download/plugins/git-client/latest/git-client.hpi
RUN curl -O https://updates.jenkins-ci.org/download/plugins/git/latest/git.hpi
RUN curl -O https://updates.jenkins-ci.org/download/plugins/ansicolor/latest/ansicolor.hpi
RUN curl -O https://updates.jenkins-ci.org/download/plugins/multiple-scms/latest/multiple-scms.hpi
RUN curl -O https://updates.jenkins-ci.org/download/plugins/github-api/latest/github-api.hpi
RUN curl -O https://updates.jenkins-ci.org/download/plugins/github/latest/github.hpi

# get maven 3.2.2
RUN wget --no-verbose -O /tmp/apache-maven-3.2.2.tar.gz http://archive.apache.org/dist/maven/maven-3/3.2.2/binaries/apache-maven-3.2.2-bin.tar.gz

# verify checksum
RUN echo "87e5cc81bc4ab9b83986b3e77e6b3095 /tmp/apache-maven-3.2.2.tar.gz" | md5sum -c

# install maven
RUN tar xzf /tmp/apache-maven-3.2.2.tar.gz -C /opt/
RUN ln -s /opt/apache-maven-3.2.2 /opt/maven
RUN ln -s /opt/maven/bin/mvn /usr/local/bin
RUN rm -f /tmp/apache-maven-3.2.2.tar.gz
ENV MAVEN_HOME /opt/maven
