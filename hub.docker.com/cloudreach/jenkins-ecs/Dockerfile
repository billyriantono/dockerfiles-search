# Always use a specific jenkins version, never use 'latest' or 'alpine' tags
FROM jenkins/jenkins:2.173
LABEL Description="Cloudreach Internal Jenkins Build Server - Alpine version"

# Disable Plugins installation wizard step & Install our default plugins
COPY plugins_list.txt /usr/share/jenkins/ref/plugins.txt
RUN echo 2.0 > /usr/share/jenkins/ref/jenkins.install.UpgradeWizard.state && \
    /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt
