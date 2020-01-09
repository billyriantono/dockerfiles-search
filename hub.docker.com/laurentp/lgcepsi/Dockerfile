from debian 
run apt-get update && \
    apt-get install -y maven openjdk-7-jdk && \
    apt-get clean 
add pom.xml /srv/lgc/
workdir /srv/lgc/
run mvn install
add src /srv/lgc/src/
expose 8080
cmd mvn jetty:run
