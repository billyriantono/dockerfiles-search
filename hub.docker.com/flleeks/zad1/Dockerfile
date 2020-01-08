FROM java:8
COPY . /
ENV MYSQL_ROOT_PASSWORD=root
EXPOSE 3306 3306
WORKDIR /
RUN javac DockerConnectMySQL.java
CMD ["java", "-classpath", "mysql-connector-java-8.0.13.jar:.","DockerConnectMySQL"]
