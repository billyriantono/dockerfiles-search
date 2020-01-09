FROM openjdk:8-jdk-alpine
ENV APPROOT="/usr/nobody"
WORKDIR $APPROOT    
ADD target/hostnameapp-1.0.jar $APPROOT
EXPOSE 8080
ENTRYPOINT ["java"]
CMD ["-jar","-Xmx128m","-Xms128m","-Djava.security.egd=file:/dev/./urandom", "/usr/nobody/hostnameapp-1.0.jar"]