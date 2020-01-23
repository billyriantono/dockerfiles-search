FROM java:7
ENV foo bar
COPY src /home/root/javahelloworld/src
WORKDIR /home/root/javahelloworld
RUN mkdir bin
RUN mkdir image
RUN javac -d  bin src/helloworld.java
ENTRYPOINT ["java",  "-cp", "bin", "helloworld"]
