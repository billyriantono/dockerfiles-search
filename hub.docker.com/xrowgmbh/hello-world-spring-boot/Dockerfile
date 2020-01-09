FROM maven:3-jdk-8
ADD ./ /opt/hello-world
RUN cd /opt/hello-world && \
    mvn clean package && \
    mv ./target/myproject-0.0.1-SNAPSHOT.jar /myproject-0.0.1-SNAPSHOT.jar
ADD ./run.sh /run.sh
RUN chmod a+x /run.sh
EXPOSE 8080:8080
CMD /run.sh
