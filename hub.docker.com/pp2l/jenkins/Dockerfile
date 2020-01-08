FROM jenkins:1.651.1

COPY configuration/ /usr/share/jenkins/ref/
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/ref/plugins.txt

USER root

RUN curl -OL https://github.com/openshift/origin/releases/download/v1.1.5/openshift-origin-client-tools-v1.1.5-847f337-linux-64bit.tar.gz \
    && tar xzvf openshift-origin-client-tools-v1.1.5-847f337-linux-64bit.tar.gz \
    && mv */oc /usr/local/bin/ \
    && rm -rf openshift-origin-client-tools-*

USER jenkins
