FROM java:7
COPY src/HelloWorld.java /
ENV  MYVAR ciao
RUN javac HelloWorld.java
ENTRYPOINT ["java","HelloWorld"]
