FROM jenkins/jenkins:2.207

# Distributed Builds plugins
RUN /usr/local/bin/install-plugins.sh ssh-slaves

# Bitbucket integration
RUN /usr/local/bin/install-plugins.sh bitbucket


# Artifacts
RUN /usr/local/bin/install-plugins.sh htmlpublisher

# UI
RUN /usr/local/bin/install-plugins.sh greenballs
RUN /usr/local/bin/install-plugins.sh simple-theme-plugin

# Scaling
RUN /usr/local/bin/install-plugins.sh kubernetes

#Install command-launcher dependency trilead-api
RUN /usr/local/bin/install-plugins.sh trilead-api

# install Maven
USER root
RUN apt-get update && apt-get install -y maven
USER jenkins

