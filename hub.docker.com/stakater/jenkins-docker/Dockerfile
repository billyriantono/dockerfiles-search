FROM fabric8/jenkins-docker:2.2.335

COPY plugins.txt /usr/share/jenkins/plugins2.txt
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins2.txt

# lets configure Jenkins with some defaults
COPY config/*.xml /usr/share/jenkins/ref/
