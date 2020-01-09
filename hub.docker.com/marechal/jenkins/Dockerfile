FROM jenkins
USER root
COPY plugins.txt /tmp/
USER jenkins
RUN plugins.sh /tmp/plugins.txt
