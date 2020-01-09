FROM java:7
COPY HelloWorld.java /
RUN apt update && \
		apt install -y vim
RUN javac HelloWorld.java
ENTRYPOINT java HelloWorld


