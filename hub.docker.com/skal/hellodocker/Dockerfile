FROM java:7
WORKDIR /home/root
RUN mkdir javahelloworld
WORKDIR /home/root/javahelloworld
RUN mkdir src bin
COPY src /home/root/javahelloworld/src
RUN javac -d bin src/Hello.java
ENTRYPOINT ["java", "-cp", "bin", "Hello"]
