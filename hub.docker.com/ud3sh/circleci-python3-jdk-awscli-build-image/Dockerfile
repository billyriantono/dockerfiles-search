FROM circleci/python:3.6.7

USER root

#Install AWS-cli, OpenJDK Java, and Maven
ENV MAVEN_VERSION=3.6.0 MAVEN_HOME=/usr/lib/mvn

RUN apt-get install openjdk-8-jre && \
    wget http://archive.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz && \
    tar -zxvf apache-maven-$MAVEN_VERSION-bin.tar.gz && \
    rm apache-maven-$MAVEN_VERSION-bin.tar.gz && \
    mv apache-maven-$MAVEN_VERSION /usr/lib/mvn && \
    pip install awscli --upgrade --user && \
    mv ~/.local /home/circleci/.local && \
    chown -R circleci:circleci /home/circleci/.local

USER circleci
ENV PATH=$PATH:$MAVEN_HOME/bin:/home/circleci/.local/bin

CMD ["/bin/sh"]