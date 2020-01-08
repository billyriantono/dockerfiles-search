FROM openjdk:8-jre

# Add the jar with all the dependencies
# Maven creates container-test.jar in the target folder of my workspace.
# We need this in some location - say - /usr/share/tag folder of the container

#ADD  target/container-test.jar /usr/share/tag/container-test.jar

# Command line to execute the test
ENTRYPOINT mvn test -DsuiteXmlFile=Sanity.xml -Dremote=true