FROM ubuntu:16.04
LABEL "Maintainer"="Paulo"
RUN apt-get update && \
    apt-get install -y python-software-properties software-properties-common && \
    apt-get update && \
    apt-get install -y iputils-ping && \
    apt-get update && \
    add-apt-repository ppa:webupd8team/java && \
    apt-get install -y mysql-client && \
    apt-get update && \
    apt-get install -y default-jdk maven && \
    apt-get update

ADD . /usr/local/vegan
RUN cd /usr/local/vegan && mvn assembly:assembly

#CMD ["java", "-cp", "/usr/local/vegan/target/vegan-v1.0-jar-with-dependencies.jar", "com.veganapp.App"]
CMD ["mvn", "exec:java"]

