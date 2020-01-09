FROM java:8  
COPY ./Plik.java ./
COPY ./mysql-connector-java-8.0.13.jar /mysql-connector-java-8.0.13.jar
RUN javac Plik.java
CMD ["java", "-classpath", "mysql-connector-java-8.0.13.jar:.","Plik"]
