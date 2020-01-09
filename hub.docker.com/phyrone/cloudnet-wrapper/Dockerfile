FROM openjdk:11-jre
WORKDIR /app/
RUN wget -O /bin/Cloudnet-Wrapper.jar https://ci.cloudnetservice.eu/job/CloudNetService/job/CloudNet/job/master/lastSuccessfulBuild/artifact/cloudnet-wrapper/target/CloudNet-Wrapper.jar
CMD ["java","-jar","/bin/Cloudnet-Wrapper.jar"]
