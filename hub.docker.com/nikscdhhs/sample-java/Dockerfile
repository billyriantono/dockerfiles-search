FROM openjdk:8-slim
COPY . /usr/local/sample-java
WORKDIR /usr/local/sample-java/src/gov/scdhhs/sample/java/app
RUN javac MaxValue.java
CMD ["java", "MaxValue"]