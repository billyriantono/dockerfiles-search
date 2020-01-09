# Version: 0.0.1

	FROM dockerfile/java:openjdk-7-jdk

	MAINTAINER Siva "siva@example.com"

	RUN apt-get update

	ADD dockertest.jar /data/dockertest.jar


	CMD ["java", "-jar", "dockertest.jar"]

	EXPOSE 8080





















# Deploying our own jar file

	#Version: 0.0.1

	#FROM ubuntu:14.04
	
	#MAINTAINER Siva "siva@example.com"

	#RUN apt-get update

	# installing JDK
	#RUN apt-get install -y openjdk-7-jdk

	#ADD dockertest.jar /

	#ENTRYPOINT ["java", "-jar", "dockertest.jar"]

	#CMD ["java", "-jar", "dockertest.jar"]
	#EXPOSE 8080







# example from  http://blog.xebia.com/2014/10/29/how-to-dockerize-your-dropwizard-application/

	#FROM dockerfile/java:openjdk-7-jdk

	#ADD dropwizard-example-1.0.0.jar /data/dropwizard-example-1.0.0.jar

	#ADD example.keystore /data/example.keystore

	#ADD example.yml /data/example.yml

	#RUN java -jar dropwizard-example-1.0.0.jar db migrate /data/example.yml

	#CMD java -jar dropwizard-example-1.0.0.jar server /data/example.yml

	#EXPOSE 8080
