FROM centos:7
MAINTAINER Alex Szczuczko <aszczucz@redhat.com>

RUN yum install -y java-1.8.0-openjdk-devel which && \
    yum clean all

ENV PATH="/opt/apache-maven/bin:${PATH}"

ENTRYPOINT ["mvn", "-B"]
CMD ["install"]

RUN curl -o mvn.tar.gz http://www.apache.org/dist/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz && \
    tar -xf mvn.tar.gz -C /opt/ && \
    rm mvn.tar.gz && \
    mv /opt/apache-maven-3.3.9/ /opt/apache-maven && \
    mkdir /opt/apache-maven/conf/settings && \
    mv /opt/apache-maven/conf/settings.xml /opt/apache-maven/conf/settings && \
    ln -s /opt/apache-maven/conf/settings/settings.xml /opt/apache-maven/conf/settings.xml && \
    groupadd --gid 2000 maven && \
    useradd --uid 2000 --gid 2000 maven

USER 2000:2000
