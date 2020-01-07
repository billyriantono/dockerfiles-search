# latest oracle openjdk is the basis
FROM oracle/openjdk:8

# set maintainer
MAINTAINER Murat Artim "muratartim@gmail.com"

# copy jar
COPY target/dist/EclipseTactics.jar eclipseTactics/EclipseTactics.jar

# copy libraries
COPY target/dist/libs eclipseTactics/libs

# copy default options
COPY options /root/.eclipseTactics/options

# change to server directory
WORKDIR /eclipseTactics

# start server
CMD ["java", "-Xms256m", "-Xmx1024m", "-XX:+UseStringDeduplication", "-Xverify:none", "-server", "-XX:+UseParallelGC", "-jar", "EclipseTactics.jar"]

# To build the docker image: (from where this file is located)
# docker image build -t muratartim/eclipsetactics_client:latest .

# To run the container on mac (from where eclipsetactics_docker_client_mac.sh file is located)
# sh eclipsetactics_docker_client_mac.sh
