# Set base image as official Ubuntu 16.04
FROM ubuntu:18.04

# OPTIONAL: Auther of docker file
LABEL "Auther"="https://github.com/sanjay-namdeo/"

# Install updates on Ubuntu
RUN apt update && apt-get install -y software-properties-common

# Install curl, wget and vim
RUN apt-get -y install curl wget vim

# Install Java 11
RUN cd /opt; \
    wget --no-check-certificate -c --header "Cookie: oraclelicense=accept-securebackup-cookie" https://download.oracle.com/otn-pub/java/jdk/11.0.1+13/90cf5d8f270a4347a95050320eef3fb7/jdk-11.0.1_linux-x64_bin.tar.gz \
    && tar zxf jdk-11.0.1_linux-x64_bin.tar.gz \
    && ln -s jdk-11 java \
    && rm -f jdk-11.0.1_linux-x64_bin.tar.gz

# Set JAVA_HOME and add it to environment PATH
ENV JAVA_HOME=/opt/jdk-11.0.1
ENV PATH="$PATH:$JAVA_HOME/bin"

# Install Maven
RUN apt-get install maven -y

# Copy sample maven app to image
COPY /sample-maven-app/ /usr/local/sample-maven-app

# Move inside project folder in image and use maven assembly to build a jar file
RUN cd /usr/local/sample-maven-app && mvn clean install assembly:single

# Execute jar file
CMD ["java", "-jar", "/usr/local/sample-maven-app/target/sample-maven-app-1.0-jar-with-dependencies.jar"]

