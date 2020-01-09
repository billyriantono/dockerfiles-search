# Install OpenJDK-8
FROM java:8

RUN apt-get install -y openjdk-8-jdk 
COPY java/Hello.java /
RUN javac Hello.java

ENTRYPOINT ["java", "Hello"]
