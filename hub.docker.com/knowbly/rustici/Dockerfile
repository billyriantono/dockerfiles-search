FROM ubuntu:18.04

## Some utilities
RUN apt-get update -y && \
    apt-get install -y build-essential libfuse-dev libcurl4-openssl-dev libxml2-dev pkg-config libssl-dev mime-support automake libtool wget tar git unzip
RUN apt-get install lsb-release -y  && apt-get install zip -y && apt-get install vim -y

## Install JAVA and tomcat8
RUN apt-get -y update && apt-get -y upgrade && \
    apt-get install default-jre -y 
RUN mkdir /usr/local/tomcat
RUN wget http://www-us.apache.org/dist/tomcat/tomcat-8/v8.5.50/bin/apache-tomcat-8.5.50.tar.gz -O /tmp/tomcat.tar.gz
RUN cd /tmp && tar xvfz tomcat.tar.gz
RUN cp -Rv /tmp/apache-tomcat-8.5.50/* /usr/local/tomcat/ 

## Copy Installers and .war file
WORKDIR /root
RUN mkdir installer scripts webapps
COPY installer /root/installer
COPY scripts /root/scripts
COPY RusticiEngine.war /root/webapps/RusticiEngine.war
COPY files /root/files
COPY keys /root/keys

# Set AWS Env variables
ARG AWS_ACCESS_KEY_ID=AKIAQ2EJABMEFKDSE5NN
ENV AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY
ARG AWS_SECRET_ACCESS_KEY=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
ENV AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY
ARG S3_MOUNT_DIRECTORY=/usr/local/tomcat/webapps/courses
ENV S3_MOUNT_DIRECTORY=$S3_MOUNT_DIRECTORY

## Expose listening port
EXPOSE 8080 

# Start deploy process
RUN chmod 777 /root/scripts/setup.sh
WORKDIR /root/scripts/
CMD ["./setup.sh"]

