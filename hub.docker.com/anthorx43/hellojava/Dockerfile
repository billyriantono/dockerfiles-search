FROM java:7

WORKDIR /home/root/javahello
RUN mkdir bin src
COPY src/Hello.java ./src
RUN javac -d bin src/Hello.java
RUN touch /tmp/test

ENTRYPOINT ["java","-cp","bin","Hello"]

