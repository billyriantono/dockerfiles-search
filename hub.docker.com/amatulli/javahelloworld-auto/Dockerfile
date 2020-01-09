FROM java:8
# coucou
WORKDIR /home/root/javahelloworld
COPY src src
RUN mkdir bin && javac -d bin src/HelloWorld.java
ENV FOO bar
CMD ["java", "-cp", "bin", "HelloWorld"]

