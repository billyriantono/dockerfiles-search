FROM develar/java:8u45

MAINTAINER Sérgio Duarte (smd@fct.unl.pt)

ADD jar/TaxiKafkaProducer.jar /root/TaxiKafkaProducer.jar
# Set environment variables.
ENV HOME /root

# Define working directory.
WORKDIR /root

ENTRYPOINT ["java", "-Djava.security.egd=file:/dev/urandom"]

# Define default command.
CMD ["-Dzk.connect=zookeeper:2181", "-Dbootstrap.servers=kafka-1:9092", "-jar", "/root/TaxiKafkaProducer.jar", "/debs/sorted_data.csv.gz"]
