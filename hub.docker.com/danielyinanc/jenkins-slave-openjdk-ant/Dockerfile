FROM evarga/jenkins-slave

RUN sudo apt-get update
RUN sudo apt-get install -y openjdk-6-jdk
RUN sudo apt-get install wget unzip
RUN wget http://archive.apache.org/dist/ant/binaries/apache-ant-1.7.1-bin.tar.gz
RUN mkdir /ant
RUN tar xvf apache-ant-1.7.1-bin.tar.gz -C /ant

WORKDIR /ant/apache-ant-1.7.1
ENV ANT_HOME /ant/apache-ant-1.7.1
ENV JAVA_HOME /usr/lib/jvm/java-6-openjdk-amd64

CMD ["/bin/bash"]