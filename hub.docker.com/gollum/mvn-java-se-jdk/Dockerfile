FROM centos:7

RUN curl -l -o jdk-8u212-linux-x64.tar.gz https://packages.mhonyi.com/java/jdk-8u212-linux-x64.tar.gz && \
tar zxvf jdk-8u212-linux-x64.tar.gz && mv jdk1.8.0_212 /opt && ln -snf /opt/jdk1.8.0_212 /usr/local/jdk1.8 && \
echo 'pathmunge /usr/local/jdk1.8/bin' > /etc/profile.d/jdk1.8.sh && \
echo 'export JAVA_HOME=/usr/local/jdk1.8' >> /etc/profile.d/jdk1.8.sh && rm -rf jdk-8u212-linux-x64.tar.gz 

RUN curl -l -o apache-maven-3.6.2-bin.tar.gz http://apache.mirror.amaze.com.au/maven/maven-3/3.6.2/binaries/apache-maven-3.6.2-bin.tar.gz && \
tar zxvf apache-maven-3.6.2-bin.tar.gz && mv apache-maven-3.6.2 /opt && ln -snf  /opt/apache-maven-3.6.2 /usr/local/mvn && \
echo 'pathmunge /usr/local/mvn/bin' > /etc/profile.d/mvn.sh && source /etc/profile && rm -rf apache-maven-3.6.2-bin.tar.gz

ADD .m2 /tmp/.m2
RUN mv /tmp/.m2 $HOME/.m2

CMD cd $HOME;whoami;ls -a
