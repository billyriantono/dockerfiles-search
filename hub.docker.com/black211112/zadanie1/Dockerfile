FROM java:8
LABEL maintainer="OP"
COPY ./Main.java ./Main.java
COPY ./mysql-connector-java-8.0.13.jar ./mysql-connector-java-8.0.13.jar
RUN javac ./Main.java
CMD ["java","-cp","mysql-connector-java-8.0.13.jar:.","Main","init"]
