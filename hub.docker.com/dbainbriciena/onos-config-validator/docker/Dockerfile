FROM java:8
COPY src /home/root/java/src
WORKDIR /home/root/java
RUN mkdir bin
RUN javac -d bin src/Book.java src/Library.java


#CMD ["java", "Library"]