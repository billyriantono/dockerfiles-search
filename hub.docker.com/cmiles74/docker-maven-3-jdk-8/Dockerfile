from maven:3-jdk-8

# install docker
RUN apt-get update && apt-get install -y docker
copy ca-certs /ca-certs
RUN keytool -import -file /ca-certs/gdig2.crt.pem -keystore /usr/lib/jvm/java-8-openjdk-amd64/jre/lib/security/cacerts -storepass "changeit"
