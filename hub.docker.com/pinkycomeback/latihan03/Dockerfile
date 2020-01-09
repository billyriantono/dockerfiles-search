FROM java:8
COPY src /home/root/javahelloword/src
WORKDIR	/home/root/javahelloword
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
ENTRYPOINT ["java","-cp","bin","Helloworld"]

