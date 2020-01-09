FROM openjdk:11  
COPY . /var/www/java  
COPY target/classes /var/www/java  
WORKDIR /var/www/java  
ENTRYPOINT [ "sh", "-c", "java $JAVA_OPTS -Dnloops=-1 \"com.handf.dockertest.DockerTest\" \"AA\" $my_params" ]
RUN javac src/main/java/com/handf/dockertest/DockerTest.java  
CMD ["java", "com.handf.dockertest.DockerTest"]  
