FROM jenkins/jenkins:lts-centos

# Plugins for build
RUN /usr/local/bin/install-plugins.sh ssh-slaves

# Plugins for better UX (not mandatory)
RUN /usr/local/bin/install-plugins.sh ansicolor
RUN /usr/local/bin/install-plugins.sh greenballs

# Plugin for scaling Jenkins agents
RUN /usr/local/bin/install-plugins.sh kubernetes

USER jenkins