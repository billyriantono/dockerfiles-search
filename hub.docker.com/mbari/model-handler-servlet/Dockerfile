# This is a Docker build file that starts with a Tomcat image and builds and deploys an application
# that listens for HTTP requests and transforms them into events that are published to RabbitMQ
FROM tomcat:9.0.11-jre8

# First let's add the source directory inside the container
ADD . /root/model-handler-servlet

# Now run the commands to build up the image (all run as root)
RUN apt-get upgrade -y && \
    apt-get update -y && \
    apt-get install -y openjdk-8-jdk \
    maven && \
    apt-get clean all && \
    cd /root/model-handler-servlet && \
    mkdir /root/.m2 && \
    cp ./settings.xml /root/.m2 && \
    mvn package && \
    cp ./target/model-handler.war /usr/local/tomcat/webapps/model-handler.war

CMD ["catalina.sh", "run"]
