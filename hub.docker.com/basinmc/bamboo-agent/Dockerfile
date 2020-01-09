FROM basinmc/bamboo-agent:base

USER root
RUN apt-get update && \
    apt-get install -y software-properties-common && \
    add-apt-repository -y ppa:openjdk-r/ppa && \
    apt-get update && \
    apt-get install -y openjdk-11-jdk-headless && \
    update-alternatives --set java /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java && \
    apt-get remove -y software-properties-common && \
    apt-get clean

USER ${BAMBOO_USER}
RUN ${BAMBOO_USER_HOME}/bamboo-update-capability.sh "system.jdk.JDK 11" /usr/lib/jvm/java-11-openjdk-amd64

ENTRYPOINT ["./entrypoint.sh"]
