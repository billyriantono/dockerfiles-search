FROM java:8
MAINTAINER kfisz
COPY . /var/www/java
WORKDIR /var/www/java
RUN javac Sample.java
CMD ["java","-classpath","mysql-connector-java-8.0.13.jar:.","Sample"]
