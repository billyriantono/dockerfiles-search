FROM java:7
COPY src /home/root/hellofromjava/src 
WORKDIR /home/root/hellofromjava
RUN mkdir bin
RUN javac -d bin src/HelloWorld.java
ENTRYPOINT ["java", "-cp", "bin", "HelloWorld"]
