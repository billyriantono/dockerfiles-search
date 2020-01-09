FROM jenkins/jenkins:latest

# Artifacts
RUN /usr/local/bin/install-plugins.sh htmlpublisher

# UI
RUN /usr/local/bin/install-plugins.sh simple-theme-plugin
RUN /usr/local/bin/install-plugins.sh locale

# Integration

RUN /usr/local/bin/install-plugins.sh github-pullrequest

# Setup theme
COPY ./plugins/theme/neo-light.css /var/jenkins_home/userContent/neo-light.css
COPY ./plugins/theme/org.codefirst.SimpleThemeDecorator.xml /var/jenkins_home/org.codefirst.SimpleThemeDecorator.xml

# Setup language
COPY ./plugins/locale/locale.xml /var/jenkins_home/locale.xml
