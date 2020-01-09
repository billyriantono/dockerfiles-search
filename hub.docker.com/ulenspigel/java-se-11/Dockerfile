FROM centos:latest
RUN yum -y install wget && \
    cd /home && \
    wget --no-cookies --no-check-certificate --header "Cookie: oraclelicense=accept-securebackup-cookie" \
    http://download.oracle.com/otn-pub/java/jdk/11.0.2+9/f51449fcd52f4d52b93a989c5c56ed3c/jdk-11.0.2_linux-x64_bin.tar.gz && \
    tar xzfv jdk-11.0.2_linux-x64_bin.tar.gz && \
    rm -f jdk-11.0.2_linux-x64_bin.tar.gz
RUN alternatives --install /usr/bin/java java /home/jdk-11.0.2/bin/java 2 && \
    alternatives --install /usr/bin/jar jar /home/jdk-11.0.2/bin/jar 2 && \
    alternatives --install /usr/bin/javac javac /home/jdk-11.0.2/bin/javac 2
ENV JAVA_HOME=/home/jdk-11.0.2
ENV PATH=$PATH:$JAVA_HOME
