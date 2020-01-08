FROM jenkins:alpine

# Pre-installed plugins
COPY plugins.txt /usr/share/jenkins/plugins.txt
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins.txt

# No executors on the master Jenkins node
COPY executors.groovy /usr/share/jenkins/ref/init.groovy.d/
