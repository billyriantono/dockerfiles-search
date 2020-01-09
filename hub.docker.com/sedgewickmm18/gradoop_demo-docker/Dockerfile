FROM ubuntu:latest

run apt-get update && apt-get -y upgrade && apt-get -y install git openjdk-8-jdk && apt-get -y install maven

run git clone https://github.com/dbs-leipzig/gradoop_demo

run cd gradoop_demo && mvn clean install && mvn exec:java -Dexec.mainClass="org.gradoop.demo.server.Server"

run sed -i 's/System.in.read()/int inChar;while ((inChar = System.in.read()) == -1){}/' /gradoop_demo/src/main/java/org/gradoop/demo/server/Server.java 
run cat /gradoop_demo/src/main/java/org/gradoop/demo/server/Server.java

run cd gradoop_demo && mvn clean install

expose 2342

copy docker_start.sh /
cmd /docker_start.sh
