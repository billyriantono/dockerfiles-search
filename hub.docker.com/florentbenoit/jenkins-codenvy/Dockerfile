FROM codenvy/ubuntu_jdk8 
RUN cd /tmp && git clone https://github.com/jenkinsci/jenkins && cd jenkins && mvn clean install -pl war -am -DskipTests && rm -rf $HOME/.m2/repository/org/jenkins-ci/main && rm -rf /tmp/jenkins
