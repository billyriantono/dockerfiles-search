FROM csanchez/jenkins-for-volumes

COPY config/plugins.txt /usr/share/jenkins/plugins.txt
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins.txt

# remove executors in master
COPY config/executors.groovy /usr/share/jenkins/ref/init.groovy.d/executors.groovy
