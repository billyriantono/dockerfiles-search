FROM trepr/centos-base:latest
LABEL maintainer="TRE-PR/SECTI/COSIS/Seção de Desenvolvimento de Sistemas <sds@tre-pr.jus.br>" \
      description="Imagem docker base JDK8"

# Install java packages
RUN yum update -y \
    && yum -y install \
        java-1.8.0-openjdk-devel \
    && yum clean all

# Set the JAVA_HOME variable to make it clear where Java is located
ENV JAVA_HOME /usr/lib/jvm/java
