FROM openshift/jenkins-slave-base-centos7:v3.11

ENV JDK_VERSION=11.0.1 \
MAVEN_VERSION=3.6.1 \
PATH=$PATH:/opt/maven/bin

RUN wget https://download.java.net/java/GA/jdk11/13/GPL/openjdk-${JDK_VERSION}_linux-x64_bin.tar.gz && \
tar -zxf openjdk-${JDK_VERSION}_linux-x64_bin.tar.gz -C /usr/lib/ && \
rm -f openjdk-${JDK_VERSION} && \
update-alternatives --install /usr/bin/java java /usr/lib/jdk-${JDK_VERSION}/bin/java 20000 --family java-1.11-openjdk.x86_64 && \
update-alternatives --set java /usr/lib/jdk-${JDK_VERSION}/bin/java && \
wget https://www-eu.apache.org/dist/maven/maven-3/${MAVEN_VERSION}/binaries/apache-maven-${MAVEN_VERSION}-bin.zip && \
unzip -q apache-maven-${MAVEN_VERSION}-bin.zip -d /opt && \
mv /opt/apache-maven-${MAVEN_VERSION} /opt/maven && \
rm apache-maven-${MAVEN_VERSION}-bin.zip && \
mkdir -p $HOME/.m2 && \
chown -R 1001:0 $HOME && \
chmod -R g+rw $HOME

ADD run-jnlp-client /usr/local/bin/

RUN chmod +x /usr/local/bin/run-jnlp-client
USER 1001