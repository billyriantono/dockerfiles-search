FROM openjdk:7-jdk

# Fetch h2o shannon
RUN \
  wget http://h2o-release.s3.amazonaws.com/h2o-dev/rel-shannon/1/h2o-dev-3.0.0.1.zip -O /opt/h2o.zip && \
  unzip -d /opt /opt/h2o.zip && \
  rm /opt/h2o.zip && \
  cd /opt && \
  cd `find . -name 'h2o.jar' | sed 's/.\///;s/\/h2o.jar//g'` && \
  cp h2o.jar /opt && \
  wget https://s3.amazonaws.com/h2o-training/mnist/train.csv.gz && \
  gunzip train.csv.gz

# Define a mountable data directory
# VOLUME \
#   ["/data"]

# Define the working directory
# WORKDIR \
#   /data

EXPOSE 54321
EXPOSE 54322

#ENTRYPOINT ["java", "-Xmx4g", "-jar", "/opt/h2o.jar"]
# Define default command

CMD \
  ["java", "-Xmx1g", "-jar", "/opt/h2o.jar"]

