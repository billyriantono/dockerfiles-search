FROM java:7
RUN mkdir -p /home/root/javahelloword/src
RUN pwd
RUN ls -lart
#COPY ./HelloWorld.java /home/root/javahelloword/src
#RUN mkdir -p /home/root/javahelloword/bin; (cd /home/root/javahelloword; javac -d bin src/HelloWorld.java)
RUN apt-get update && apt-get install -y vim
ENTRYPOINT ["java", "-cp", "/home/root/javahelloword/bin", "HelloWorld"]
