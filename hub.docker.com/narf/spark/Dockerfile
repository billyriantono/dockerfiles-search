FROM lukasz/docker-scala

RUN apt-get update
RUN apt-get -y install wget curl
RUN mkdir /spark

WORKDIR /spark

RUN wget http://d3kbcqa49mib13.cloudfront.net/spark-0.9.1.tgz
RUN tar -xzf spark-0.9.1.tgz
RUN cd spark-0.9.1 && ./sbt/sbt assembly

ENTRYPOINT ["/spark/spark-0.9.1/bin/spark-class", "org.apache.spark.deploy.worker.Worker"] 
