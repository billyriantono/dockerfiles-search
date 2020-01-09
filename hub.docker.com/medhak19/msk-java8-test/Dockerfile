FROM java:8
RUN apt-get update && \
	apt-get upgrade -y && \
	apt-get install -y vim
COPY src/ /usr/src/myapp
WORKDIR /usr/src/myapp
RUN javac com/test/TestJava.java
CMD ["java", "com.test.TestJava"]