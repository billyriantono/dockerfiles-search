FROM jenkinsci/blueocean:latest
USER root
COPY plugins.txt /plugins.txt

RUN /bin/bash -l -c "/usr/local/bin/install-plugins.sh  `cat /plugins.txt | tr \"\\n\" \" \"`"

# Add the required Ansible packages
RUN apk add ansible rsync

USER jenkins
