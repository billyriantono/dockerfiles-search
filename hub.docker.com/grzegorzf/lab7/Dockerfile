FROM java:8
WORKDIR /
COPY ./mysql-connector-java-5.1.47.jar /mysql-connector-java-5.1.47.jar
COPY ./App.java /App.java
COPY ./s.sh /s.sh
ENV CLASSPATH=/mysql-connector-java-5.1.47.jar:${CLASSPATH}

RUN chmod +x /s.sh
ENTRYPOINT ["./s.sh"]
