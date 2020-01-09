from java:7

#RUN apt-get update
#Run apt-get install -y wget
COPY HelloWorld.java /
RUN javac HelloWorld.java
ENTRYPOINT ["java","HelloWorld"]
#CMD ["wget","www.google.com"]


