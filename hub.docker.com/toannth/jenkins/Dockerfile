from jenkins:2.32.3

COPY plugins.txt /usr/share/jenkins/
RUN set -ex; \
   /usr/local/bin/install-plugins.sh $(cat /usr/share/jenkins/plugins.txt | tr '\n' ' ')
