FROM saltstack/centos-6
MAINTAINER Alexis MP "alexis.mp@gmail.com"

# Update list of packages
RUN yum check-update

# install Java 7
RUN su -c "yum --assumeyes install java-1.7.0-openjdk-devel"

# set a bunch of environment variables
ENV JAVA_HOME /usr/lib/jvm/java-1.7.0-openjdk.x86_64
ENV PATH $JAVA_HOME/bin:$PATH
